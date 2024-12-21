-- Biblioteca de Interface Gráfica
local Library = loadstring(game:HttpGet("https://pastebin.com/raw/FsJak6AT"))() -- Exemplo de biblioteca GUI

-- Criando a Janela Principal
local Window = Library.CreateLib("Universal Script", "DarkGreen")

-- Ícone de Caveira para Abrir/Fechar o Menu
local ToggleKey = Enum.KeyCode.LeftControl
local ToggleButton = Instance.new("ImageButton")
ToggleButton.Name = "ToggleButton"
ToggleButton.Parent = game.CoreGui
ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ToggleButton.BorderSizePixel = 0
ToggleButton.Position = UDim2.new(0, 0, 0.5, -25)
ToggleButton.Size = UDim2.new(0, 50, 0, 50)
ToggleButton.Image = "rbxassetid://1257105241162256539"

local UserInputService = game:GetService("UserInputService")
local isMenuOpen = true

UserInputService.InputBegan:Connect(function(input)
    if input.KeyCode == ToggleKey then
        isMenuOpen = not isMenuOpen
        if isMenuOpen then
            Window:Show()
        else
            Window:Hide()
        end
    end
end)

-- Funções para Aimbot, Silent Aim e No Clip
local aimbotActive = false
local silentAimActive = false
local noClipActive = false

-- Aimbot
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

-- Silent Aim
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

-- No Clip
local function noClip()
    while noClipActive do
        for _, v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
            if v:IsA("BasePart") then
                v.CanCollide = false
            end
        end
        wait()
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

GeralSection:NewToggle("No Clip", "Atravessar paredes", function(state)
    noClipActive = state
    if noClipActive then
        noClip()
    end
end)

