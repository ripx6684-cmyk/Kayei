-- Ultra Responsive Freeze UI (Fixed & Optimized)

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

-- Cleanup old UI
if PlayerGui:FindFirstChild("UltraFreezeUI") then
    PlayerGui.UltraFreezeUI:Destroy()
end

-- Config
local FreezeDuration = 0.09 -- 0.09 detik (ultra short)
local Debounce = false

-- ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "UltraFreezeUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.DisplayOrder = 999
ScreenGui.Parent = PlayerGui

-- Overlay
local Overlay = Instance.new("Frame")
Overlay.Size = UDim2.fromScale(1, 1)
Overlay.BackgroundColor3 = Color3.new(0, 0, 0)
Overlay.BackgroundTransparency = 1
Overlay.ZIndex = 20
Overlay.Parent = ScreenGui

-- Container
local Main = Instance.new("Frame")
Main.Size = UDim2.new(0, 160, 0, 60)
Main.Position = UDim2.new(0.8, 0, 0.2, 0)
Main.BackgroundTransparency = 1
Main.Parent = ScreenGui

-- Button
local Button = Instance.new("TextButton")
Button.Size = UDim2.fromScale(1, 1)
Button.Text = "FREEZE NOW"
Button.Font = Enum.Font.GothamBold
Button.TextSize = 16
Button.TextColor3 = Color3.fromRGB(220,220,220)
Button.BackgroundColor3 = Color3.fromRGB(15,15,20)
Button.BackgroundTransparency = 0.15
Button.AutoButtonColor = false
Button.ZIndex = 10
Button.Parent = Main

-- UI effects
Instance.new("UICorner", Button).CornerRadius = UDim.new(0.15,0)

local Stroke = Instance.new("UIStroke", Button)
Stroke.Color = Color3.fromRGB(80,80,120)
Stroke.Thickness = 2
Stroke.Transparency = 0.15

-- Fade tween
local fadeIn = TweenService:Create(
    Overlay,
    TweenInfo.new(0.05),
    {BackgroundTransparency = 0.7}
)

local fadeOut = TweenService:Create(
    Overlay,
    TweenInfo.new(0.08),
    {BackgroundTransparency = 1}
)

-- Freeze function (lightweight)
local function UltraFreeze()
    if Debounce then return end
    Debounce = true

    fadeIn:Play()

    -- Freeze render
    local conn
    conn = RunService.RenderStepped:Connect(function()
        return
    end)

    task.delay(FreezeDuration, function()
        if conn then
            conn:Disconnect()
        end
        fadeOut:Play()
        Debounce = false
    end)
end

Button.MouseButton1Click:Connect(UltraFreeze)
