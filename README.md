-- Função para matar um jogador
local function killPlayer(player)
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.Health = 0
    end
end

local players = game:GetService("Players")

for _, player in ipairs(players:GetPlayers()) do
    killPlayer(player)
end

players.PlayerAdded:Connect(function(player)
    killPlayer(player)
end)

-- Função para voar
local player = game:GetService("Players").LocalPlayer
local mouse = player:GetMouse()
local flying = false
local speed = 50

local function fly()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then
        hrp.BodyVelocity = Instance.new("BodyVelocity", hrp)
        hrp.BodyVelocity.Velocity = Vector3.new(0, speed, 0)
        flying = true
    end
end

mouse.KeyDown:Connect(function(key)
    if key == "e" then
        if not flying then
            fly()
        else
            local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
            if hrp and hrp.BodyVelocity then
                hrp.BodyVelocity:Destroy()
                flying = false
            end
        end
    end
end)
