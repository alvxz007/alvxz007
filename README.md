-- Variáveis globais
local aimlockActive = false
local target

-- Função para ativar/desativar o aimlock
local function toggleAimlock()
    aimlockActive = not aimlockActive
end

-- Cria um botão para ativar/desativar o aimlock
local screenGui = Instance.new("ScreenGui")
local toggleButton = Instance.new("TextButton")

screenGui.Parent = game.CoreGui
toggleButton.Parent = screenGui
toggleButton.Size = UDim2.new(0, 200, 0, 50)
toggleButton.Position = UDim2.new(0.5, -100, 0.9, -25)
toggleButton.Text = "Ativar Aimlock"
toggleButton.MouseButton1Click:Connect(function()
    toggleAimlock()
    if aimlockActive then
        toggleButton.Text = "Desativar Aimlock"
    else
        toggleButton.Text = "Ativar Aimlock"
    end
end)

-- Função de aimlock
local function aimlock()
    while aimlockActive do
        local player = game.Players.LocalPlayer
        local mouse = player:GetMouse()
        local targetPart = target and target:FindFirstChild("HumanoidRootPart")

        if targetPart then
            mouse.TargetFilter = target
            player.Character.HumanoidRootPart.CFrame = CFrame.new(player.Character.HumanoidRootPart.Position, targetPart.Position)
        end
        wait()
    end
end

-- Função para encontrar o alvo mais próximo
local function findTarget()
    local player = game.Players.LocalPlayer
    local closestDistance = math.huge

    for _, v in pairs(game.Players:GetPlayers()) do
        if v ~= player and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
            local distance = (player.Character.HumanoidRootPart.Position - v.Character.HumanoidRootPart.Position).magnitude
            if distance < closestDistance then
                closestDistance = distance
                target = v.Character
            end
        end
    end
end

-- Loop para atualizar o aimlock
game:GetService("RunService").RenderStepped:Connect(function()
    if aimlockActive then
        findTarget()
        aimlock()
    end
end)
