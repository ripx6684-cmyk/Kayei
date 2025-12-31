-- Random Freeze / Fake Crash (Delta Compatible)

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local Player = Players.LocalPlayer

-- Cleanup GUI
local PlayerGui = Player:WaitForChild("PlayerGui")
if PlayerGui:FindFirstChild("UltraFreezeUI") then
	PlayerGui.UltraFreezeUI:Destroy()
end

-- GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "UltraFreezeUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = PlayerGui

local Button = Instance.new("TextButton")
Button.Size = UDim2.new(0,160,0,60)
Button.Position = UDim2.new(0.8,0,0.2,0)
Button.Text = "RANDOM FREEZE"
Button.Font = Enum.Font.GothamBold
Button.TextSize = 16
Button.TextColor3 = Color3.fromRGB(235,235,235)
Button.BackgroundColor3 = Color3.fromRGB(20,20,25)
Button.Parent = ScreenGui

Instance.new("UICorner", Button).CornerRadius = UDim.new(0.2,0)
Instance.new("UIStroke", Button).Thickness = 2

-- SETTINGS
local MinFreeze = 0.3
local MaxFreeze = 0.6
local Busy = false

-- Random freeze function
local function RandomFreeze()
	if Busy then return end
	Busy = true

	local char = Player.Character
	if not char then Busy = false return end

	local humanoid = char:FindFirstChildOfClass("Humanoid")
	local root = char:FindFirstChild("HumanoidRootPart")
	if not humanoid or not root then Busy = false return end

	-- Random duration
	local FreezeDuration = math.random(
		math.floor(MinFreeze * 100),
		math.floor(MaxFreeze * 100)
	) / 100

	-- Save state
	local oldWalk = humanoid.WalkSpeed
	local oldJump = humanoid.JumpPower

	-- Freeze
	root.Anchored = true
	humanoid.WalkSpeed = 0
	humanoid.JumpPower = 0
	UserInputService.ModalEnabled = true

	task.wait(FreezeDuration)

	-- Restore
	root.Anchored = false
	humanoid.WalkSpeed = oldWalk
	humanoid.JumpPower = oldJump
	UserInputService.ModalEnabled = false

	Busy = false
end

Button.MouseButton1Click:Connect(RandomFreeze)
