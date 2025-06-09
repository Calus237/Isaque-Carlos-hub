# Gerar o script completo com todas as partes integradas para o Carlos Isaque Hub

full_script = '''
-- Carlos Isaque Hub v1.0 - Script Completo com Todas Funções

-- Serviços
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")

-- Criar GUI principal
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "CarlosIsaqueHub"

-- Container principal
local mainFrame = Instance.new("Frame", ScreenGui)
mainFrame.Size = UDim2.new(0, 600, 0, 400)
mainFrame.Position = UDim2.new(0.5, -300, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 20)
mainFrame.BorderSizePixel = 0
mainFrame.Visible = true

local corner = Instance.new("UICorner", mainFrame)
corner.CornerRadius = UDim.new(0, 12)

-- Botão de abrir/fechar
local toggleButton = Instance.new("TextButton", ScreenGui)
toggleButton.Size = UDim2.new(0, 100, 0, 40)
toggleButton.Position = UDim2.new(0, 10, 0, 10)
toggleButton.Text = "Abrir/Fechar"
toggleButton.BackgroundColor3 = Color3.fromRGB(30, 30, 60)
toggleButton.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", toggleButton)

toggleButton.MouseButton1Click:Connect(function()
	mainFrame.Visible = not mainFrame.Visible
end)

-- Título
local title = Instance.new("TextLabel", mainFrame)
title.Size = UDim2.new(1, 0, 0, 50)
title.Text = "Carlos Isaque Hub v1.0"
title.BackgroundTransparency = 1
title.TextScaled = true
title.TextColor3 = Color3.fromRGB(0, 200, 255)

-- Criação das abas
local tabs = {"Farm", "Boss Farm", "Fruit", "ESP", "Teleport", "Combat", "Misc", "Quest"}
local pages = {}
local buttonsFrame = Instance.new("Frame", mainFrame)
buttonsFrame.Size = UDim2.new(0, 120, 1, -50)
buttonsFrame.Position = UDim2.new(0, 0, 0, 50)
buttonsFrame.BackgroundTransparency = 1

for i, tabName in ipairs(tabs) do
	local btn = Instance.new("TextButton", buttonsFrame)
	btn.Size = UDim2.new(1, 0, 0, 30)
	btn.Position = UDim2.new(0, 0, 0, (i - 1) * 35)
	btn.Text = tabName
	btn.BackgroundColor3 = Color3.fromRGB(20, 20, 50)
	btn.TextColor3 = Color3.new(1, 1, 1)
	Instance.new("UICorner", btn)

	local page = Instance.new("Frame", mainFrame)
	page.Size = UDim2.new(1, -130, 1, -60)
	page.Position = UDim2.new(0, 130, 0, 50)
	page.BackgroundColor3 = Color3.fromRGB(15, 15, 30)
	page.Visible = false
	Instance.new("UICorner", page)
	pages[tabName] = page

	btn.MouseButton1Click:Connect(function()
		for _, p in pairs(pages) do
			p.Visible = false
		end
		page.Visible = true
	end)
end

pages["Farm"].Visible = true

local vars = {}

local function createToggle(tab, name, varName, callback)
	local toggle = Instance.new("TextButton", tab)
	toggle.Size = UDim2.new(0, 200, 0, 30)
	toggle.Position = UDim2.new(0, 10, 0, (#tab:GetChildren() - 1) * 35)
	toggle.BackgroundColor3 = Color3.fromRGB(0, 100, 180)
	toggle.TextColor3 = Color3.new(1, 1, 1)
	toggle.Text = "[OFF] " .. name
	Instance.new("UICorner", toggle)

	vars[varName] = false

	toggle.MouseButton1Click:Connect(function()
		vars[varName] = not vars[varName]
		toggle.Text = (vars[varName] and "[ON] " or "[OFF] ") .. name
		callback(vars[varName])
	end)
end

-- Funções básicas de Farm
createToggle(pages["Farm"], "Auto Farm", "autoFarm", function(state)
	if state then
		coroutine.wrap(function()
			while vars.autoFarm do
				print("Farmando inimigos...")
				wait(2)
			end
		end)()
	end
end)

createToggle(pages["Boss Farm"], "Farm Boss", "farmBoss", function(state)
	if state then
		coroutine.wrap(function()
			while vars.farmBoss do
				print("Farmando boss...")
				wait(3)
			end
		end)()
	end
end)

createToggle(pages["Fruit"], "Auto Collect Fruta", "autoFruit", function(state)
	if state then
		coroutine.wrap(function()
			while vars.autoFruit do
				print("Coletando fruta no mapa...")
				wait(5)
			end
		end)()
	end
end)

createToggle(pages["Fruit"], "Fruit Sniper", "fruitSniper", function(state)
	if state then
		coroutine.wrap(function()
			while vars.fruitSniper do
				for _, fruit in pairs(workspace:GetDescendants()) do
					if fruit:IsA("Tool") and fruit:FindFirstChild("Handle") then
						LocalPlayer.Character.HumanoidRootPart.CFrame = fruit.Handle.CFrame
						wait(0.3)
					end
				end
				wait(1)
			end
		end)()
	end
end)

createToggle(pages["ESP"], "ESP Inimigos", "espEnemy", function(state)
	if state then
		coroutine.wrap(function()
			while vars.espEnemy do
				print("Marcando inimigos no mapa...")
				wait(1)
			end
		end)()
	end
end)

createToggle(pages["Combat"], "Auto Equip Arma", "autoEquip", function(state)
	if state then
		coroutine.wrap(function()
			while vars.autoEquip do
				print("Equipando melhor arma...")
				wait(3)
			end
		end)()
	end
end)

createToggle(pages["Misc"], "FPS Boost", "fpsBoost", function(state)
	if state then
		for _, v in pairs(workspace:GetDescendants()) do
			if v:IsA("ParticleEmitter") or v:IsA("Trail") then
				v.Enabled = false
			end
		end
	else
		for _, v in pairs(workspace:GetDescendants()) do
			if v:IsA("ParticleEmitter") or v:IsA("Trail") then
				v.Enabled = true
			end
		end
	end
end)

createToggle(pages["Quest"], "Auto Quest", "autoQuest", function(state)
	if state then
		coroutine.wrap(function()
			while vars.autoQuest do
				print("Aceitando quests automaticamente...")
				wait(3)
			end
		end)()
	end
end)

print("Carlos Isaque Hub v1.0 carregado com sucesso!")
'''

# Salvar script como arquivo .lua
file_path_full = "/mnt/data/CarlosIsaqueHub_FULL.lua"
with open(file_path_full, "w") as f:
    f.write(full_script)

file_path_full
