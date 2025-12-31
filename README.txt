--[[ 
    Fake Start Lag - Draconic Hub Style (Evade)
    Client-side only | Safe
]]

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer

-- UI
local gui = Instance.new("ScreenGui")
gui.IgnoreGuiInset = true
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local bg = Instance.new("Frame", gui)
bg.Size = UDim2.fromScale(1,1)
bg.BackgroundColor3 = Color3.fromRGB(0,0,0)

local text = Instance.new("TextLabel", bg)
text.Size = UDim2.fromScale(1,1)
text.BackgroundTransparency = 1
text.TextColor3 = Color3.fromRGB(255,0,0)
text.TextScaled = true
text.Font = Enum.Font.GothamBold
text.Text = "Draconic Hub\nInitializing..."

-- Ép cảm giác lag (RenderStepped overload)
local lagTime = 5.5
local start = tick()

while tick() - start < lagTime do
	for i = 1, 80000 do
		local a = math.sin(i) * math.random()
	end
	RunService.RenderStepped:Wait()
end

-- Fake module loading
local messages = {
	"Loading Core...",
	"Injecting Modules...",
	"Optimizing Evade...",
	"Finalizing..."
}

for _,msg in ipairs(messages) do
	text.Text = "Draconic Hub\n"..msg
	task.wait(0.6)
end

-- Fade out
for i = 1, 20 do
	bg.BackgroundTransparency += 0.05
	text.TextTransparency += 0.05
	task.wait()
end

gui:Destroy()
