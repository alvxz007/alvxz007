-- Variáveis e funções principais
local Library = loadstring(game:HttpGet("https://pastebin.com/raw/uTms3xYs"))() -- Link para um exemplo de biblioteca de interface gráfica

local Window = Library.CreateLib("Blox Fruits Script", "DarkGreen") -- Cria a janela principal

-- Seção Geral
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

-- (Adicione as outras opções de farm aqui)

-- Seção Itens e Missões
local ItensMissoes = Window:NewTab("Itens e Missões")
local ItensMissoesSection = ItensMissoes:NewSection("Itens e Missões")

ItensMissoesSection:NewToggle("Auto All Itens", "Coleta automática de todos os itens", function(state)
    if state then
        print("Auto All Itens Ativado")
    else
        print("Auto All Itens Desativado")
    end
end)

-- (Adicione as outras opções de itens e missões aqui)

-- Seção Status
local Status = Window:NewTab("Status")
local StatusSection = Status:NewSection("Status")

StatusSection:NewButton("Auto Set Status", "Configura automaticamente o status", function()
    print("Auto Set Status Ativado")
end)

-- Seção ESP
local ESP = Window:NewTab("ESP")
local ESPSection = ESP:NewSection("ESP")

ESPSection:NewToggle("ESP Baús", "Mostrar baús", function(state)
    if state then
        print("ESP Baús Ativado")
    else
        print("ESP Baús Desativado")
    end
end)

-- (Adicione as outras opções de ESP aqui)

-- Seção Raid
local Raid = Window:NewTab("Raid")
local RaidSection = Raid:NewSection("Raid")

RaidSection:NewToggle("Auto Farm Raid", "Farm automático de raids", function(state)
    if state then
        print("Auto Farm Raid Ativado")
    else
        print("Auto Farm Raid Desativado")
    end
end)

-- Seção Jogadores
local Jogadores = Window:NewTab("Jogadores")
local JogadoresSection = Jogadores:NewSection("Jogadores")

-- (Adicione funções para jogadores se necessário)

-- Funções adicionais
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


-- Loop para atualizar o aimlock
game:GetService("RunService").RenderStepped:Connect(function()
    if aimlockActive then
        findTarget()
        aimlock()
    end
end)
