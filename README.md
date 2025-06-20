-- 🟡 AEGONA Full Script with All Functions

-- 🔧 Global Toggles
_G.Farm1 = false
_G.AutoHarvest = false
_G.HoneyFarm = false
_G.NoClip = false
_G.SelectFruit = "All"

_G.AutoBuy = {
	-- 🌱 seeds
    ["Pepper"] = false,
    ["Mushroom"] = false,
    ["EmberLily"] = false,
    ["SugarApple"] = false,
	-- 🐝 event
    ["SunFlowerPack"] = false,
    ["BeeEgg"] = false,
	-- ⚙️ gear
    ["LightningRod"] = false,
    ["GodlySprinkler"] = false,
    ["MasterSprinkler"] = false,
	-- 🥚 egg
    ["Common Egg"] = false,
    ["Uncommon Egg"] = false,
    ["Rare Egg"] = false,
    ["Legendary Egg"] = false,
    ["Mythical Egg"] = false,
    ["Bug Egg"] = false,
}

_G.EGG_Check = true
_G.EGG_Buy = true
_G.EggSpawn = {
	["Egg1"] = nil,
	["Egg2"] = nil,
	["Egg3"] = nil,
}

local player = game.Players.LocalPlayer
local virtualUser = game:GetService("VirtualUser")

-- ฟังก์ชันนี้จะถูกเรียกเมื่อ Roblox แจ้งว่า player AFK (Idle)
player.Idled:Connect(function()
    -- กดเมาส์คลิกเล็กน้อยเพื่อรีเซ็ตสถานะ AFK
    virtualUser:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
    wait(0.1)
    virtualUser:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
    print("Anti AFK triggered!")
end)


-- 🖥️ Load UI
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/memejames/elerium-v2-ui-library//main/Library", true))()
local window = library:AddWindow("🐝 Aegona | อีโก้น่า Thai version", {
    main_color = Color3.fromRGB(41, 74, 122),
    min_size = Vector2.new(300, 346),
    can_resize = false,
})

-- 📋 Tabs
local features = window:AddTab("🌾 MAIN")
features:Show()
features:AddLabel("🌱 - Farm -")
features:AddSwitch("🚜 TP Pollinated | วาร์ป หาผลไม้ สถานะผึ้ง", function(bool) _G.Farm1 = bool end)




local dropdown = features:AddDropdown("🍈 SelectFruit | เลือกผล", function(text) _G.SelectFruit = text end)
dropdown:Add("All")
dropdown:Add("Coconut")
dropdown:Add("Mango")

features:AddLabel("🍯 - Event Farm -")
features:AddSwitch("🐝 Honey Farm | ฟาร์มน้ำผึ้ง", function(bool) _G.HoneyFarm = bool end)

features:AddLabel("📍 - Teleport -")
features:AddButton("📦 Teleport to Event | วาร์ปไปที่ อีเว้น", function()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-83.79, 2.99, -11.43)
end)

features:AddButton("⚙️ Teleport to Gear shop | วาร์ปไปร้าน เกียร์", function()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-287.23, 3.00, -33.22)
end)

local features2 = window:AddTab("🛍️ SHOP")
features2:Show()

-- Seed Shop
local folder = features2:AddFolder("🌿 Seeds Shop เมล็ดพืช 🌱")
folder:AddLabel("📦 - Seeds เมล็ดพืช -")
folder:AddSwitch("🌶️ Pepper | พริก", function(bool) _G.AutoBuy["Pepper"] = bool end)
folder:AddSwitch("🍄 Mushroom | เห็ด", function(bool) _G.AutoBuy["Mushroom"] = bool end)
folder:AddSwitch("🔥 EmberLily | เอ็มเบอร์", function(bool) _G.AutoBuy["EmberLily"] = bool end)
folder:AddSwitch("🍎 SugarApple | ชูก้า แอปเปิ้ล", function(bool) _G.AutoBuy["SugarApple"] = bool end)

-- Gear Shop
local folder2 = features2:AddFolder("⚙️ Gears Shop เกียร์ ⚙️")
folder2:AddLabel("🛠️ - Gears Shop เกียร์ -")
folder2:AddSwitch("⚡ LightningRod | สายล่อฟ้า", function(bool) _G.AutoBuy["LightningRod"] = bool end)
folder2:AddSwitch("🌊 GodlySprinkler | ก็อตลี่ สปริงเกอร์", function(bool) _G.AutoBuy["GodlySprinkler"] = bool end)
folder2:AddSwitch("💧 MasterSprinkler | มาสเตอร์ สปริงเกอร์", function(bool) _G.AutoBuy["MasterSprinkler"] = bool end)

-- Egg Shop
local folder3 = features2:AddFolder("🥚 Egg Shop ไข่ 🥚")
folder3:AddLabel("🧺 - Egg Shop ไข่ -")
folder3:AddSwitch("🥚 Common Egg | ไข่ คอมมอน", function(bool) _G.AutoBuy["Common Egg"] = bool end)
folder3:AddSwitch("🟩 Uncommon Egg | ไข่ อันคอมมอน", function(bool) _G.AutoBuy["Uncommon Egg"] = bool end)
folder3:AddSwitch("🔷 Rare Egg | ไข่ แรร์", function(bool) _G.AutoBuy["Rare Egg"] = bool end)
folder3:AddSwitch("🟡 Legendary Egg | ไข่ รีเจน", function(bool) _G.AutoBuy["Legendary Egg"] = bool end)
folder3:AddSwitch("🟣 Mythical Egg | ไข่ มิสติเคิ้ล", function(bool) _G.AutoBuy["Mythical Egg"] = bool end)
folder3:AddSwitch("🐞 Bug Egg | ไข่ แมลง", function(bool) _G.AutoBuy["Bug Egg"] = bool end)

-- Even Shop
local folder4 = features2:AddFolder("🐝 Even Shop อีเว้นต์ 🐝")
folder4:AddLabel("🌼 - Even Shop อีเว้นต์ -")
folder4:AddSwitch("🌻 Sunflower Pack | ซอง ทานตะวัน", function(bool) _G.AutoBuy["SunFlowerPack"] = bool end)
folder4:AddSwitch("🐝 Bee Egg | ไข่ ผึ้ง", function(bool) _G.AutoBuy["BeeEgg"] = bool end)

--🔷 Game Services
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Event = ReplicatedStorage.GameEvents
local plr = Players.LocalPlayer
local plrname = plr.Name



--🔷 Game Services
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Event = ReplicatedStorage:WaitForChild("GameEvents")
local plr = Players.LocalPlayer
local plrname = plr.Name

--🔷 Identify MyFarm
local function FindFarm()
    for _, v in pairs(workspace.Farm:GetDescendants()) do
        if v:IsA("StringValue") and v.Name == "Owner" and v.Value == plrname then
            if v.Parent.Parent.Parent.Name == "Farm" then
                v.Parent.Parent.Parent.Name = "MyFarm"
            end
        end
    end
end
FindFarm()

local FarmFolder = workspace.Farm:WaitForChild("MyFarm")
local Important = FarmFolder:WaitForChild("Important")
local PlantsPhysical = Important:WaitForChild("Plants_Physical")

--🔷 Farm Teleport Logic
spawn(function()
    while true do
        _G.NoClip = _G.Farm1
        if _G.Farm1 then
		   
            local rootpart = plr.Character:WaitForChild("HumanoidRootPart")
            for _, plantModel in pairs(PlantsPhysical:GetDescendants()) do
                if plantModel:IsA("Model") and plantModel:FindFirstChild("Grow") and plantModel:FindFirstChild("Fruits") then
                    for _, fruit in pairs(plantModel.Fruits:GetDescendants()) do
                        if fruit:IsA("Model") and (_G.SelectFruit == "All" or fruit.Name == _G.SelectFruit) and fruit:FindFirstChild("PrimaryPart") then
                            local primary = fruit.PrimaryPart
                            if primary:FindFirstChild("Swirls") then
							   if _G.Farm1 == true then
								rootpart.CFrame = primary.CFrame * CFrame.new(0, 4, 0)
								_G.AutoHarvest = true
                                task.wait(0.5)
								
								_G.AutoHarvest = false
							else
								break
								
							   end
                            end
                        end
                    end
                end
            end
        end
        task.wait(1)
    end
end)

local SafeParts = {
	"Baseplate",
	"Terrain",
}

-- 🌟 สคริปต์เปิด/ปิด Noclip
spawn(function()
	while true do
		if _G.NoClip then
			local character = game.Players.LocalPlayer.Character
			if character then
				for _, part in pairs(character:GetDescendants()) do
					if part:IsA("BasePart") then
						local touching = part:GetTouchingParts()
						local shouldCollide = false

						for _, touchingPart in pairs(touching) do
							if table.find(SafeParts, touchingPart.Name) then
								shouldCollide = true
								break
							end
						end

						part.CanCollide = not shouldCollide
					end
				end
			end
		else
			-- ปิด noclip แล้วคืนค่า CanCollide
			local character = game.Players.LocalPlayer.Character
			if character then
				for _, part in pairs(character:GetDescendants()) do
					if part:IsA("BasePart") then
						part.CanCollide = true
					end
				end
			end
		end
		task.wait(0.1)
	end
end)

--🔷 Honey Farm
spawn(function()
    while true do
        if _G.HoneyFarm then
            local backpack = plr:WaitForChild("Backpack")
            local character = plr.Character or plr.CharacterAdded:Wait()
            local humanoid = character:FindFirstChildOfClass("Humanoid")
            for _, tool in ipairs(backpack:GetChildren()) do
                if tool:IsA("Tool") and tool.Name:lower():find("pollinate") then
                    local weight = tool:FindFirstChild("Weight")
                    if weight and tonumber(weight.Value) < 50 then
                        humanoid:EquipTool(tool)
                        Event.HoneyMachineService_RE:FireServer("MachineInteract")
                        task.wait(1.5)
                    end
                end
            end
        end
        task.wait(0.1)
    end
end)

--🔷 Auto Harvest
local function CanHarvest(plant)
    local prompt = plant:FindFirstChild("ProximityPrompt", true)
    return prompt and prompt.Enabled
end

local function HarvestPlant(plant)
    local prompt = plant:FindFirstChild("ProximityPrompt", true)
    if prompt then fireproximityprompt(prompt) end
end

local function CollectHarvestable(parent, plants)
    local pos = plr.Character:GetPivot().Position
    for _, plant in ipairs(parent:GetChildren()) do
        if plant:FindFirstChild("Fruits") then
            CollectHarvestable(plant.Fruits, plants)
        end
        local variant = plant:FindFirstChild("Variant")
        if variant and (variant.Value == "Gold" or variant.Value == "Rainbow") then continue end
        if (pos - plant:GetPivot().Position).Magnitude > 10 then continue end
        if CanHarvest(plant) then table.insert(plants, plant) end
    end
end

local function HarvestPlants()
    local plants = {}
    CollectHarvestable(PlantsPhysical, plants)
    for _, plant in ipairs(plants) do HarvestPlant(plant) end
end

coroutine.wrap(function()
    while true do
        if _G.AutoHarvest then HarvestPlants() end
        task.wait(0.2)
    end
end)()


_G.EggSpawn = {
	["Egg1"] = nil,
	["Egg2"] = nil,
	["Egg3"] = nil,
}

--🔷 Auto Buy
spawn(function()
    while true do
        if _G.AutoBuy["SunFlowerPack"] then Event.BuyEventShopStock:FireServer("Flower Seed Pack") end
        if _G.AutoBuy["BeeEgg"] then Event.BuyEventShopStock:FireServer("Bee Egg") end
        if _G.AutoBuy["SugarApple"] then Event.BuySeedStock:FireServer("Sugar Apple") end
        if _G.AutoBuy["EmberLily"] then Event.BuySeedStock:FireServer("Ember Lily") end
        if _G.AutoBuy["Pepper"] then Event.BuySeedStock:FireServer("Pepper") end
        if _G.AutoBuy["Mushroom"] then Event.BuySeedStock:FireServer("Mushroom") end
        if _G.AutoBuy["LightningRod"] then Event.BuyGearStock:FireServer("Lightning Rod") end
        if _G.AutoBuy["MasterSprinkler"] then Event.BuyGearStock:FireServer("Master Sprinkler") end
        if _G.AutoBuy["GodlySprinkler"] then Event.BuyGearStock:FireServer("Godly Sprinkler") end
        task.wait(3)
    end
end)

-- ฟังก์ชันตั้งชื่อ Location ให้ตรงกับพิกัด
function SetNumberEgg()
	local egg1Pos = Vector3.new(-289.041259765625, 2.8755276203155518, 3.7303857803344727)
	local egg2Pos = Vector3.new(-289.0312194824219, 2.79752779006958, 7.740394592285156)
	local egg3Pos = Vector3.new(-289.03924560546875, 2.79752779006958, 11.770347595214844)

	for _, v in pairs(workspace.NPCS["Pet Stand"].EggLocations:GetChildren()) do
		if v:IsA("Part") then
			if (v.Position - egg1Pos).Magnitude < 0.01 then
				v.Name = "Location1"
			elseif (v.Position - egg2Pos).Magnitude < 0.01 then
				v.Name = "Location2"
			elseif (v.Position - egg3Pos).Magnitude < 0.01 then
				v.Name = "Location3"
			end
		end
	end
end

-- ฟังก์ชันอัปเดตและแสดงความหายากของไข่
function UpdateEggRarity()
	SetNumberEgg()
	wait(0.5)

	for i = 1, 3 do
		local eggLocation = workspace.NPCS["Pet Stand"].EggLocations["Location"..i]
		local rarityText = eggLocation:FindFirstChild("PetInfo") and eggLocation.PetInfo:FindFirstChild("SurfaceGui") and eggLocation.PetInfo.SurfaceGui:FindFirstChild("RarityTextLabel")
		if rarityText then
			_G.EggSpawn["Egg"..i] = rarityText.Text
			print("Egg"..i.." Rarity: " .. rarityText.Text)

		else
			_G.EggSpawn["Egg"..i] = nil
			print("Egg"..i.." Rarity: (Not Found)")
		end
	end
end

-- ฟังก์ชันเช็คและซื้อไข่ตามเงื่อนไข AutoBuy
function CheckAndBuyEggs()
	for i = 1, 3 do
		local rarity = _G.EggSpawn["Egg"..i]
		local key = rarity and (rarity .. " Egg")
		if key and _G.AutoBuy[key] then
			print("AutoBuy: Buying", key, "from Egg"..i)
			game:GetService("ReplicatedStorage").GameEvents.BuyPetEgg:FireServer(i)
		end
	end
end

-- วนลูปอัปเดต EggSpawn
spawn(function()
	while _G.EGG_Check do
		UpdateEggRarity()
		wait(10)
	end
end)

-- วนลูปสั่งซื้อไข่ตาม AutoBuy
spawn(function()
	while _G.EGG_Buy do
		CheckAndBuyEggs()
		wait(2)
	end
end)
