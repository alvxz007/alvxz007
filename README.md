-- Biblioteca de Interface Gráfica
local Library = loadstring(game:HttpGet("https://pastebin.com/raw/FsJak6AT"))() -- Exemplo de biblioteca GUI

-- Criando a Janela Principal
local Window = Library.CreateLib("Blox Fruits Script", "DarkGreen")

-- Ícone de Caveira para Abrir/Fechar o Menu
local ToggleKey = Enum.KeyCode.LeftControl
local ToggleButton = Instance.new("ImageButton")
ToggleButton.Name = "ToggleButton"
ToggleButton.Parent = game.CoreGui
ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ToggleButton.BorderSizePixel = 0
ToggleButton.Position = UDim2.new(0, 0, 0.5, -25)
ToggleButton.Size = UDim2.new(0, 50, 0, 50)
ToggleButton.Image = "rbxassetid://YOUR_SKULL_ICON_ASSET_ID" -- Substitua pelo ID do seu ícone de caveira

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

-- Aba Geral
local Geral = Window:NewTab("Geral")
local GeralSection = Geral:NewSection("Geral")

GeralSection:NewToggle("Auto Farm Level", "Farm automático de nível", function(state)
    if state then
        print("Auto Farm Level Ativado")
    else
        print("Auto Farm Level Desativado")
    end
end)

GeralSection:NewToggle("Auto Farm Money", "Farm automático de dinheiro", function(state)
    if state then
        print("Auto Farm Money Ativado")
    else
        print("Auto Farm Money Desativado")
    end
end)

-- (Adicionar todas as outras funções do menu Geral aqui)

-- Aba Itens e Missões
local ItensMissoes = Window:NewTab("Itens e Missões")
local ItensMissoesSection = ItensMissoes:NewSection("Itens e Missões")

ItensMissoesSection:NewToggle("Auto All Itens", "Coleta automática de todos os itens", function(state)
    if state then
        print("Auto All Itens Ativado")
    else
        print("Auto All Itens Desativado")
    end
end)

-- (Adicionar todas as outras funções do menu Itens e Missões aqui)

-- Aba Status
local Status = Window:NewTab("Status")
local StatusSection = Status:NewSection("Status")

StatusSection:NewButton("Auto Set Status", "Configura automaticamente o status", function()
    print("Auto Set Status Ativado")
end)

-- Aba ESP
local ESP = Window:NewTab("ESP")
local ESPSection = ESP:NewSection("ESP")

ESPSection:NewToggle("ESP Baús", "Mostrar baús", function(state)
    if state then
        print("ESP Baús Ativado")
    else
        print("ESP Baús Desativado")
    end
end)

-- (Adicionar todas as outras funções do menu ESP aqui)

-- Aba Raid
local Raid = Window:NewTab("Raid")
local RaidSection = Raid:NewSection("Raid")

RaidSection:NewToggle("Auto Farm Raid", "Farm automático de raids", function(state)
    if state then
        print("Auto Farm Raid Ativado")
    else
        print("Auto Farm Raid Desativado")
    end
end)

-- Aba Jogadores
local Jogadores = Window:NewTab("Jogadores")
local JogadoresSection = Jogadores:NewSection("Jogadores")

-- (Adicionar funções de jogadores se necessário)

-- Funções de automação
function autoFarm()
    -- Função para auto farm
end

function autoSetStatus()
    -- Função para auto set status
end

function autoESP()
    -- Função para ESP
end

function autoRaid()
    -- Função para auto farm raid
end
