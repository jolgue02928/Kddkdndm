-- Jolgue Hub (Auto Clicker 15x/s funcional)

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer

-- GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "JolgueHub"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 100)
frame.Position = UDim2.new(0, 20, 0, 100)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true
frame.Parent = screenGui

local title = Instance.new("TextLabel")
title.Text = "Jolgue Hub (auto_click)"
title.Size = UDim2.new(1, 0, 0, 30)
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.Gotham
title.TextSize = 16
title.Parent = frame

local toggle = Instance.new("TextButton")
toggle.Text = "Ativar Auto Click"
toggle.Size = UDim2.new(1, -20, 0, 40)
toggle.Position = UDim2.new(0, 10, 0, 40)
toggle.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
toggle.Font = Enum.Font.GothamBold
toggle.TextSize = 14
toggle.Parent = frame

-- Auto Clicker Logic
local clicking = false

toggle.MouseButton1Click:Connect(function()
	clicking = not clicking
	toggle.Text = clicking and "Desativar Auto Click" or "Ativar Auto Click"
end)

-- Simula 15 cliques por segundo usando eventos de input
task.spawn(function()
	while true do
		if clicking then
			-- Simula clique real com UserInputService (alguns jogos aceitam isso melhor)
			local pos = UIS:GetMouseLocation()
			UIS.InputBegan:Fire({UserInputType = Enum.UserInputType.MouseButton1, Position = pos})
			UIS.InputEnded:Fire({UserInputType = Enum.UserInputType.MouseButton1, Position = pos})
		end
		task.wait(1 / 15)
	end
end)
