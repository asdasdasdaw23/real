local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")

-- Function to make character ignore titan collisions
local function setupAntiGrab()
    -- Wait for character to load
    if not LocalPlayer.Character then
        LocalPlayer.CharacterAdded:Wait()
    end
    
    local character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
    
    -- Set an attribute that your original script checks for
    character:SetAttribute("IgnoredTitan", true)
    
    -- Keep checking in case the attribute gets removed
    RunService.Heartbeat:Connect(function()
        if character and character:IsDescendantOf(workspace) and not character:GetAttribute("IgnoredTitan") then
            character:SetAttribute("IgnoredTitan", true)
        end
    end)
    
    -- Set up for future respawns
    LocalPlayer.CharacterAdded:Connect(function(newCharacter)
        newCharacter:SetAttribute("IgnoredTitan", true)
        character = newCharacter
    
    end)
end

setupAntiGrab()

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Function to modify values
local function modifyODMValues()
    -- Path to player's ODM values
    local ODMPath = ReplicatedStorage:FindFirstChild("ODMMaps")
    if not ODMPath then return end
    
    -- Get player's username folder
    local playerFolder = ODMPath:FindFirstChild(LocalPlayer.Name)
    if not playerFolder then return end
    
    -- Modify the values
    if playerFolder:FindFirstChild("Range") then
        playerFolder.Range.Value = 750
    end
    
    if playerFolder:FindFirstChild("MaxGas") then
        playerFolder.MaxGas.Value = 3000
    end

    if playerFolder:FindFirstChild("Gas") then
        playerFolder.Gas.Value = 3000
    end
    
    if playerFolder:FindFirstChild("Speed") then
        playerFolder.Speed.Value = 125
        
    if playerFolder:FindFirstChild("Agility") then
        playerFolder.Agility.Value = 1.4
    end

    if playerFolder:FindFirstChild("SleightofHand") then
        playerFolder.SleightofHand.Value = 1.25
    end
    
    if playerFolder:FindFirstChild("Luck") then
        playerFolder.Luck.Value = 20
    end
end
-- Apply modifications
modifyODMValues()
