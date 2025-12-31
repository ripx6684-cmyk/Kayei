-- Ultra Responsive Lag Switch for Evade - 0.09 Second Freeze
local Player = game:GetService("Players").LocalPlayer
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
-- Pastikan PlayerGui tersedia
local PlayerGui = Player:WaitForChild("PlayerGui")
-- Hapus GUI lama jika ada
if PlayerGui:FindFirstChild("UltraFreezeUI") then
PlayerGui.UltraFreezeUI:Destroy()
end
-- Buat ScreenGui baru
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "UltraFreezeUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.DisplayOrder = 999
ScreenGui.Parent = PlayerGui
-- Overlay Full Screen (Hitam Transparan)
local Overlay = Instance.new("Frame")
Overlay.Name = "Overlay"
Overlay.Size = UDim2.new(1, 0, 1, 0)
Overlay.Position = UDim2.new(0, 0, 0, 0)
Overlay.BackgroundColor3 = Color3.new(0, 0, 0)
Overlay.BackgroundTransparency = 1
Overlay.ZIndex = 20
Overlay.Parent = ScreenGui
-- Main Container
local MainContainer = Instance.new("Frame")
MainContainer.Name = "MainContainer"
MainContainer.Size = UDim2.new(0, 160, 0, 60)
MainContainer.Position = UDim2.new(0.8, 0, 0.2, 0)
MainContainer.BackgroundTransparency = 1
MainContainer.Parent = ScreenGui
-- Main Button
local FreezeButton = Instance.new("TextButton")
FreezeButton.Name = "FreezeButton"
FreezeButton.Size = UDim2.new(1, 0, 1, 0)
FreezeButton.Position = UDim2.new(0, 0, 0, 0)
FreezeButton.Text = "FREEZE NOW"
FreezeButton.Font = Enum.Font.GothamBold
FreezeButton.TextSize = 16
FreezeButton.TextColor3 = Color3.fromRGB(220, 220, 220)
FreezeButton.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
FreezeButton.BackgroundTransparency = 0.2
FreezeButton.AutoButtonColor = false
FreezeButton.ZIndex = 10
FreezeButton.Parent = MainContainer
-- Stroke Outline
local Stroke = Instance.new("UIStroke")
Stroke.Color = Color3.fromRGB(60, 60, 80)
Stroke.Thickness = 2
Stroke.Transparency = 0.1
Stroke.Parent = FreezeButton
-- Corner Radius
local Corner = Instance.new("UICorner")
Corner.CornerRadius = UDim.new(0.15, 0)
Corner.Parent = FreezeButton
-- Lag Switch Logic
local FreezeDuration = 0.30 -- Di
