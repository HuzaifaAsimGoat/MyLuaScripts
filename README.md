-- Dead Rails | Auto Collect Bonds + Show Count + "Huzaifa_Asim_Goat" Title

-- SETTINGS
local FarmSpeed = 1 -- How fast you teleport to bonds (lower = faster)

-- COUNTER FOR BONDS COLLECTED
local bondsCollected = 0

-- Create the big "Huzaifa_Asim_Goat" title in Gothic font
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player.PlayerGui

local title = Instance.new("TextLabel")
title.Parent = screenGui
title.Size = UDim2.new(0, 400, 0, 100)
title.Position = UDim2.new(0.5, -200, 0.05, 0)  -- Centered at the top
title.Text = "Huzaifa_Asim_Goat"
title.TextSize = 36
title.TextColor3 = Color3.fromRGB(255, 0, 0)  -- Red color for the text
title.Font = Enum.Font.GothamBlack  -- Gothic-style font
title.BackgroundTransparency = 1

-- Create the Bond Count label under the title
local bondCountLabel = Instance.new("TextLabel")
bondCountLabel.Parent = screenGui
bondCountLabel.Size = UDim2.new(0, 400, 0, 50)
bondCountLabel.Position = UDim2.new(0.5, -200, 0.15, 0)  -- Below the title
bondCountLabel.Text = "Bonds Collected: 0"  -- Initial text
bondCountLabel.TextSize = 24
bondCountLabel.TextColor3 = Color3.fromRGB(255, 255, 255)  -- White color for the text
bondCountLabel.Font = Enum.Font.GothamBlack  -- Gothic font for consistency
bondCountLabel.BackgroundTransparency = 1

-- FUNCTION: Teleport to Bond pickups and collect
spawn(function()
    while task.wait(FarmSpeed) do
        for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("ProximityPrompt") and v.Parent.Name == "Bond" then
                -- Teleport to the Bond
                game.Players.LocalPlayer.Character:PivotTo(v.Parent.CFrame)

                -- Wait a moment and trigger the Proximity Prompt to collect
                task.wait(0.2)
                fireproximityprompt(v)

                -- Increment bond counter
                bondsCollected = bondsCollected + 1

                -- Update the bond count text under the title
                bondCountLabel.Text = "Bonds Collected: " .. bondsCollected
            end
        end
    end
end)

-- Initial Notification to let you know it's active
game.StarterGui:SetCore("SendNotification", {
    Title = "Bonds Auto Collect Active!",
    Text = "Starting collection...",
    Duration = 5
})
# MyLuaScripts
Roblox scripts
