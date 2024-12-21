-- Biblioteca de Interface Gráfica
local Library = loadstring(game:HttpGet("https://pastebin.com/raw/FsJak6AT"))() -- Exemplo de biblioteca GUI

-- Criando a Janela Principal
local Window = Library.CreateLib("Bolotas'Hub", "DarkGreen")

-- Variáveis de Controle
local aimbotActive = false
local silentAimActive = false

-- Funções para Aimbot e Silent Aim
local function aimbot()
    if aimbotActive then
        local player = game.Players.LocalPlayer
        local mouse = player:GetMouse()
        local closestTarget

        -- Encontrar o oponente mais próximo na FOV
        for _, v in pairs(game.Players:GetPlayers()) do
            if v ~= player and v.Character and v.Character:FindFirstChild("Head") then
                local distance = (mouse.Hit.p - v.Character.Head.Position).magnitude
                if not closestTarget or distance < (mouse.Hit.p - closestTarget.Head.Position).magnitude then
                    closestTarget = v.Character
                end
            end
        end

        -- Focar a mira na cabeça do oponente
        if closestTarget then
            mouse.TargetFilter = closestTarget
            player.Character.HumanoidRootPart.CFrame = CFrame.new(player.Character.HumanoidRootPart.Position, closestTarget.Head.Position)
        end
    end
end

local function silentAim()
    if silentAimActive then
        local player = game.Players.LocalPlayer
        local mouse = player:GetMouse()
        local closestTarget

        -- Encontrar o oponente mais próximo
        for _, v in pairs(game.Players:GetPlayers()) do
            if v ~= player and v.Character and v.Character:FindFirstChild("Head") then
                local distance = (mouse.Hit.p - v.Character.Head.Position).magnitude
                if not closestTarget or distance < (mouse.Hit.p - closestTarget.Head.Position).magnitude then
                    closestTarget = v.Character
                end
            end
        end

        -- Focar a mira no oponente mais próximo
        if closestTarget then
            mouse.TargetFilter = closestTarget
            player.Character.HumanoidRootPart.CFrame = CFrame.new(player.Character.HumanoidRootPart.Position, closestTarget.Head.Position)
        end
    end
end

-- Menu para Ativar/Desativar Funções
local Geral = Window:NewTab("Geral")
local GeralSection = Geral:NewSection("Geral")

GeralSection:NewToggle("Aimbot", "Focar a mira na cabeça do oponente", function(state)
    aimbotActive = state
    if aimbotActive then
        game:GetService("RunService").RenderStepped:Connect(aimbot)
    end
end)

GeralSection:NewToggle("Silent Aim", "Focar no oponente mais próximo", function(state)
    silentAimActive = state
    if silentAimActive then
        game:GetService("RunService").RenderStepped:Connect(silentAim)
    end
end)
