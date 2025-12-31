-- ULTRA RESPONSIVE LAG SWITCH (DELTA SAFE)
local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

-- Hapus GUI lama
if PlayerGui:FindFirstChild("UltraFreezeUI") then
	PlayerGui.UltraFreezeUI:Destroy()
end

-- GUI
local ScreenGui = Instance.new("ScreenGui", PlayerGui)
ScreenGui.Name = "UltraFreezeUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.DisplayOrder = 999

-- Button Container
local Main = Instance.new("Frame", ScreenGui)
Main.Size = UDim2.new(0, 170, 0, 60)
Main.Position = UDim2.new(0.7, 0, 0.25, 0)
Main.BackgroundTransparency = 1
Main.Active = true

-- Button
local Btn = Instance.new("TextButton", Main)
Btn.Size = UDim2.new(1, 0, 1, 0)
Btn.Text = "LAG : OFF"
Btn.Font = Enum.Font.GothamBold
Btn.TextSize = 16
Btn.TextColor3 = Color3.fromRGB(230,230,230)
Btn.BackgroundColor3 = Color3.fromRGB(20,20,30)
Btn.AutoButtonColor = false

-- Style
Instance.new("UICorner", Btn).CornerRadius = UDim.new(0.2,0)
local Stroke = Instance.new("UIStroke", Btn)
Stroke.Thickness = 2
Stroke.Color = Color3.fromRGB(80,80,120)

-- =========================
-- DRAG BUTTON (MOBILE + PC)
-- =========================
local dragging, dragInput, dragStart, startPos

Main.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = Main.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

Main.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
		dragInput = input
	end
end)

UIS.InputChanged:Connect(function(input)
	if input == dragInput and dragging then
		local delta = input.Position - dragStart
		Main.Position = UDim2.new(
			startPos.X.Scale,
			startPos.X.Offset + delta.X,
			startPos.Y.Scale,
			startPos.Y.Offset + delta.Y
		)
	end
end)

-- =========================
-- LAG SWITCH LOGIC
-- =========================
local LAG_TIME = 0.9 -- detik freeze
local ENABLED = false

task.spawn(function()
	while true do
		if ENABLED then
			RunService:Set3dRenderingEnabled(false)
			task.wait(LAG_TIME)
			RunService:Set3dRenderingEnabled(true)
		end
		task.wait(0.05)
	end
end)

-- Toggle
Btn.MouseButton1Click:Connect(function()
	ENABLED = not ENABLED
	if ENABLED then
		Btn.Text = "LAG : ON"
		Btn.BackgroundColor3 = Color3.fromRGB(40,20,60)
	else
		Btn.Text = "LAG : OFF"
		Btn.BackgroundColor3 = Color3.fromRGB(20,20,30)
	end
end)
