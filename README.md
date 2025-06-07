
Script for muscle legends

-- Zebra Hub | Muscle Legends Script (Open Source)
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/watermark"))()

local Window = Library:CreateWindow("Zebra Hub - Muscle Legends")

local MainTab = Window:CreateTab("Main")
local DupeTab = Window:CreateTab("Dupe")
local AutoTab = Window:CreateTab("Auto")

-- // Variables
local autoRebirth = false
local plr = game.Players.LocalPlayer
local rs = game:GetService("ReplicatedStorage")

-- // Dupe Pets (Fake para visualização local)
DupeTab:CreateButton("Dupe Pets (Simulação)", function()
    for _, pet in pairs(plr:FindFirstChild("Pets"):GetChildren()) do
        local clone = pet:Clone()
        clone.Name = pet.Name .. "_Dupe"
        clone.Parent = plr.Pets
    end
end)

-- // Dupe Rebirths (Fake para visualização local)
DupeTab:CreateButton("Dupe Rebirths (Simulação)", function()
    local stat = plr:FindFirstChild("leaderstats")
    if stat and stat:FindFirstChild("Rebirths") then
        stat.Rebirths.Value = stat.Rebirths.Value + 1
    end
end)

-- // Auto Rebirth
AutoTab:CreateToggle("Auto Rebirth", function(state)
    autoRebirth = state
    while autoRebirth do
        local args = {
            [1] = 1 -- quantidade de rebirths
        }
        rs:WaitForChild("RebirthRemote"):FireServer(unpack(args))
        task.wait(5)
    end
end)

-- // Informações do menu
MainTab:CreateLabel("Script by ChatGPT (Open Source)")
MainTab:CreateButton("Fechar GUI", function()
    Library:Destroy()
end)
