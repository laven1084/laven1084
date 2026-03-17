loadstring([[ 
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local SoundService = game:GetService("SoundService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "laven1084FakeDonate"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 350, 0, 220)
mainFrame.Position = UDim2.new(0.5, -175, 0.5, -110)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
mainFrame.BorderSizePixel = 0
mainFrame.Visible = false
mainFrame.Parent = screenGui

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 12)
uiCorner.Parent = mainFrame

local uiGradient = Instance.new("UIGradient")
uiGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(50, 50, 60)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(20, 20, 25))
}
uiGradient.Parent = mainFrame

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 50)
title.BackgroundTransparency = 1
title.Text = "laven1084 Fake Donate"
title.TextColor3 = Color3.fromRGB(0, 255, 200)
title.TextSize = 28
title.Font = Enum.Font.GothamBold
title.Parent = mainFrame

local amountBox = Instance.new("TextBox")
amountBox.Size = UDim2.new(0.8, 0, 0, 40)
amountBox.Position = UDim2.new(0.1, 0, 0.35, 0)
amountBox.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
amountBox.TextColor3 = Color3.fromRGB(255, 255, 255)
amountBox.PlaceholderText = "Robux miktarı gir (örn: 999999)"
amountBox.Text = "1000000"
amountBox.TextSize = 18
amountBox.Font = Enum.Font.Gotham
amountBox.ClearTextOnFocus = false
amountBox.Parent = mainFrame

local boxCorner = Instance.new("UICorner")
boxCorner.CornerRadius = UDim.new(0, 8)
boxCorner.Parent = amountBox

local donateButton = Instance.new("TextButton")
donateButton.Size = UDim2.new(0.8, 0, 0, 50)
donateButton.Position = UDim2.new(0.1, 0, 0.65, 0)
donateButton.BackgroundColor3 = Color3.fromRGB(0, 200, 150)
donateButton.Text = "Fake Donate Göster!"
donateButton.TextColor3 = Color3.new(1,1,1)
donateButton.TextSize = 22
donateButton.Font = Enum.Font.GothamBold
donateButton.Parent = mainFrame

local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 10)
btnCorner.Parent = donateButton

local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 30, 0, 30)
closeButton.Position = UDim2.new(1, -35, 0, 5)
closeButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
closeButton.Text = "X"
closeButton.TextColor3 = Color3.new(1,1,1)
closeButton.TextSize = 20
closeButton.Parent = mainFrame

closeButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = false
end)

UserInputService.InputBegan:Connect(function(input, gp)
    if gp then return end
    if input.KeyCode == Enum.KeyCode.Insert then
        mainFrame.Visible = not mainFrame.Visible
    end
end)

local function showFakeDonate(amount)
    local notifGui = Instance.new("ScreenGui")
    notifGui.Name = "FakeNotif"
    notifGui.ResetOnSpawn = false
    notifGui.Parent = playerGui

    local notifFrame = Instance.new("Frame")
    notifFrame.Size = UDim2.new(0, 400, 0, 120)
    notifFrame.Position = UDim2.new(0.5, -200, -0.2, 0)
    notifFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
    notifFrame.BorderSizePixel = 0
    notifFrame.Parent = notifGui

    local notifCorner = Instance.new("UICorner")
    notifCorner.CornerRadius = UDim.new(0, 16)
    notifCorner.Parent = notifFrame

    local glow = Instance.new("ImageLabel")
    glow.Size = UDim2.new(1.2, 0, 1.2, 0)
    glow.Position = UDim2.new(-0.1, 0, -0.1, 0)
    glow.BackgroundTransparency = 1
    glow.Image = "rbxassetid://4996891970"
    glow.ImageTransparency = 0.4
    glow.ImageColor3 = Color3.fromRGB(0, 255, 200)
    glow.Parent = notifFrame

    local text = Instance.new("TextLabel")
    text.Size = UDim2.new(1, 0, 1, 0)
    text.BackgroundTransparency = 1
    text.Text = "laven1084 tarafından\\n" .. amount .. " Robux bağışlandı!"
    text.TextColor3 = Color3.fromRGB(0, 255, 200)
    text.TextSize = 32
    text.Font = Enum.Font.GothamBlack
    text.TextStrokeTransparency = 0.8
    text.TextStrokeColor3 = Color3.new(0,0,0)
    text.Parent = notifFrame

    local sound = Instance.new("Sound")
    sound.SoundId = "rbxassetid://1847661823"
    sound.Volume = 0.7
    sound.Parent = notifFrame
    sound:Play()

    local tweenIn = TweenService:Create(notifFrame, TweenInfo.new(0.8, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Position = UDim2.new(0.5, -200, 0.1, 0)})
    tweenIn:Play()

    task.wait(4)

    local tweenOut = TweenService:Create(notifFrame, TweenInfo.new(0.6, Enum.EasingStyle.Back, Enum.EasingDirection.In), {Position = UDim2.new(0.5, -200, -0.2, 0)})
    tweenOut:Play()
    tweenOut.Completed:Connect(function()
        notifGui:Destroy()
    end)
end

donateButton.MouseButton1Click:Connect(function()
    local amt = amountBox.Text
    if tonumber(amt) then
        showFakeDonate(amt)
    else
        amountBox.Text = "Geçerli sayı gir!"
        task.wait(1)
        amountBox.Text = amt
    end
end)

print("laven1084 Fake Donate yüklendi! Insert tuşu ile menüyü aç.")
]])()
