-- Biblioteca de Interface Gráfica
local Library = loadstring(game:HttpGet("https://pastebin.com/raw/FsJak6AT"))() -- Exemplo de biblioteca GUI

-- Criando a Janela Principal
local Window = Library.CreateLib("Aimlock Script", "DarkGreen")

-- Variáveis de Controle
local aimlockActive = false

-- Função de Aimlock
local function aimlock()
    while aimlockActive do
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

        -- Focar a mira na cabeça do oponente
        if closestTarget then
            mouse.TargetFilter = closestTarget
            player.Character.HumanoidRootPart.CFrame = CFrame.new(player.Character.HumanoidRootPart.Position, closestTarget.Head.Position)
        end
        wait()
    end
end

-- Menu para Ativar/Desativar Funções
local Geral = Window:NewTab("Geral")
local GeralSection = Geral:NewSection("Geral")

GeralSection:NewToggle("Aimlock", "Focar a mira na cabeça do oponente", function(state)
    aimlockActive = state
    if aimlockActive then
        game:GetService("RunService").RenderStepped:Connect(aimlock)
    end
end)

print("Aimlock Script Carregado")
