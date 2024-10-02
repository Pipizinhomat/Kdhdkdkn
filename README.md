-- Kill House Script for Brookhaven
local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")

local function flingPlayer(player)
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        local flingForce = Instance.new("BodyVelocity")
        flingForce.Velocity = Vector3.new(math.random(-100, 100), 100, math.random(-100, 100)) -- Atração aleatória
        flingForce.MaxForce = Vector3.new(4000, 4000, 4000)
        flingForce.Parent = character.HumanoidRootPart
        
        wait(0.5) -- Tempo de fling
        flingForce:Destroy() -- Remove o efeito após o tempo
    end
end

local function onPlayerAdded(player)
    player.CharacterAdded:Connect(function(character)
        wait(1) -- Espera o personagem carregar
        flingPlayer(player)
    end)
end

Players.PlayerAdded:Connect(onPlayerAdded)

-- Fling todos os jogadores quando o script rodar
for _, player in ipairs(Players:GetPlayers()) do
    onPlayerAdded(player)
end
