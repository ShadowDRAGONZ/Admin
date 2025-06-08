# Admin
-- Place this LocalScript in StarterPlayerScripts or a GUI

-- GUI setup
local screenGui = Instance.new("ScreenGui", game.Players.LocalPlayer:WaitForChild("PlayerGui"))
screenGui.Name = "RewardMenu"

local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0, 220, 0, 160)
frame.Position = UDim2.new(0.4, 0, 0.4, 0)
frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
frame.Active = true
frame.Draggable = true

-- TextBox for reward input
local inputBox = Instance.new("TextBox", frame)
inputBox.Size = UDim2.new(1, -20, 0, 40)
inputBox.Position = UDim2.new(0, 10, 0, 10)
inputBox.PlaceholderText = "Enter Reward Number (1-7)"
inputBox.Text = ""
inputBox.TextColor3 = Color3.new(1, 1, 1)
inputBox.Font = Enum.Font.SourceSans
inputBox.TextSize = 18
inputBox.BackgroundColor3 = Color3.fromRGB(70, 70, 70)

-- Send button
local sendButton = Instance.new("TextButton", frame)
sendButton.Size = UDim2.new(1, -20, 0, 40)
sendButton.Position = UDim2.new(0, 10, 0, 60)
sendButton.BackgroundColor3 = Color3.fromRGB(0, 170, 127)
sendButton.Text = "Send Reward"
sendButton.TextColor3 = Color3.new(1, 1, 1)
sendButton.Font = Enum.Font.SourceSansBold
sendButton.TextSize = 18

-- Status label
local statusLabel = Instance.new("TextLabel", frame)
statusLabel.Size = UDim2.new(1, -20, 0, 30)
statusLabel.Position = UDim2.new(0, 10, 0, 110)
statusLabel.BackgroundTransparency = 1
statusLabel.Text = ""
statusLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
statusLabel.Font = Enum.Font.SourceSans
statusLabel.TextSize = 16
statusLabel.TextWrapped = true

-- Send reward logic
sendButton.MouseButton1Click:Connect(function()
	local input = tonumber(inputBox.Text)
	if input and input >= 1 and input <= 7 then
		statusLabel.Text = "Sending Reward" .. input .. "..."
		local args = { "Reward" .. input }
		game:GetService("ReplicatedStorage"):WaitForChild("Events"):WaitForChild("Spin"):FireServer(unpack(args))
		wait(0.5)
		statusLabel.Text = "✅ Reward" .. input .. " sent successfully!"
	else
		statusLabel.Text = "❌ Please enter a number between 1 and 7."
	end
	wait(2)
	statusLabel.Text = ""
end)
