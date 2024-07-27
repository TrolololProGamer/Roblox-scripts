# Roblox-scripts
local module = {}

local DataStoreService = game:GetService("DataStoreService")
local CashDataStore = DataStoreService:GetOrderedDataStore("CashDataStore")
local Cash

game.Players.PlayerAdded:Connect(function(player)
	local leaderstats = Instance.new("Folder")
	leaderstats.Name = "leaderstats"
	leaderstats.Parent = player
	
	Cash = Instance.new("NumberValue")
	Cash.Name = "Cash"
	Cash.Parent = leaderstats
	local success, error = pcall(function()
		Cash.Value = CashDataStore:GetAsync(player.UserId)
	end)
	
	if success then
		print("Datastore worked")
	else
		warn(error)
	end
	
end)

game.Players.PlayerRemoving:Connect(function(player)
	local success, error = pcall(function()
		CashDataStore:SetAsync(player.UserId, Cash.Value)
	end)
	
	if success then
		print("Datastore worked")
	else
		warn(error)
	end
	
end)


return module
