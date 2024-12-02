local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

local Window = OrionLib:MakeWindow({
    Name = "VitinHub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "VitinHubConfig"
})
-- Função para teleportar para um jogador específico
local function TeleportToPlayer(playerName)
    local player = game:GetService("Players"):FindFirstChild(playerName)
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local localPlayer = game.Players.LocalPlayer
        if localPlayer.Character and localPlayer.Character:FindFirstChild("HumanoidRootPart") then
            localPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
        else
            print("HumanoidRootPart não encontrado para o jogador local.")
        end
    else
        print("Player não encontrado ou não está no jogo.")
    end
end

-- Função para dar permissão
local function GrantPermission(houseNumber)
    local args = {
        [1] = "GivePermissionLoopToServer",
        [2] = game:GetService("Players").LocalPlayer,
        [3] = houseNumber
    }
    local remoteEvent = game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t")
    if remoteEvent then
        remoteEvent:FireServer(unpack(args))
    else
        print("Evento remoto não encontrado.")
    end
end

-- Função para mudar o personagem para Korblox
function GiveKorblox()
    local remote = game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l")
    if remote then
        local args = {
            [1] = "CharacterChange",
            [2] = {
                [1] = 1,
                [2] = 1,
                [3] = 1,
                [4] = 37754710, -- ID da perna Korblox
                [5] = 1,
                [6] = 1
            },
            [3] = "by:Shadow Studios"
        }
        remote:FireServer(unpack(args))
    else
        print("Evento remoto não encontrado para Korblox.")
    end
end

-- Função para mudar o personagem para Zumbi
function GiveZombie()
    local remote = game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l")
    if remote then
        local args = {
            [1] = "CharacterChange",
            [2] = {
                [1] = 1,
                [2] = 1,
                [3] = 1,
                [4] = 139607718, -- ID da perna Zumbi
                [5] = 1,
                [6] = 1
            },
            [3] = "by:Shadow Studios"
        }
        remote:FireServer(unpack(args))
    else
        print("Evento remoto não encontrado para Zumbi.")
    end
end

-- Função para mudar o personagem para a perna de gelo
function GiveIceLeg()
    local remote = game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l")
    if remote then
        local args = {
            [1] = "CharacterChange",
            [2] = {
                [1] = 1,
                [2] = 1,
                [3] = 1,
                [4] = 139572789, -- ID da perna de gelo
                [5] = 1,
                [6] = 1
            },
            [3] = "by:Shadow Studios"
        }
        remote:FireServer(unpack(args))
    else
        print("Evento remoto não encontrado para a perna de gelo.")
    end
end

-- Função para assistir a um jogador específico
local function SpectatePlayer(playerName)
    local player = game:GetService("Players"):FindFirstChild(playerName)
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local camera = game.Workspace.CurrentCamera
        camera.CameraSubject = player.Character.Humanoid
        camera.CFrame = player.Character.HumanoidRootPart.CFrame
    else
        print("Player não encontrado ou não está no jogo.")
    end
end

-- Função para parar de assistir
local function StopSpectating()
    local camera = game.Workspace.CurrentCamera
    camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
end

-- Função para mudar o RolePlayName
local function ChangeNameRP(newName)
    local args = {
        [1] = "RolePlayName",
        [2] = newName
    }
    game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args))
end

-- Função para mudar a cor do RolePlayName
local function ChangeNameColorRP(color)
    local args = {
        [1] = "PickingRPNameColor",
        [2] = color
    }
    game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eColo1r"):FireServer(unpack(args))
end
-- Aba de Personagem
local CharacterTab = Window:MakeTab({
    Name = "Character",
    Icon = "rbxassetid://4483362458",
    PremiumOnly = false
})

-- Primeira Seção para Korblox
CharacterTab:AddSection({
    Name = "Korblox"
})
CharacterTab:AddButton({
    Name = "Give Korblox",
    Callback = function()
        GiveKorblox()
    end
})

-- Segunda Seção para Zumbi
CharacterTab:AddSection({
    Name = "Zombie"
})
CharacterTab:AddButton({
    Name = "Give Zombie",
    Callback = function()
        GiveZombie()
    end
})

-- Terceira Seção para Perna de Gelo
CharacterTab:AddSection({
    Name = "Ice Leg"
})
CharacterTab:AddButton({
    Name = "Give Ice Leg",
    Callback = function()
        GiveIceLeg()
    end
})

-- Aba de Permissão
local PermissionTab = Window:MakeTab({
    Name = "Permission",
    Icon = "rbxassetid://4483362458",
    PremiumOnly = false
})
PermissionTab:AddSection({
    Name = "Select House"
})
local selectedHouse = 1
PermissionTab:AddDropdown({
    Name = "Choose House",
    Options = {"House 1", "House 2", "House 3", "House 4", "House 5", "House 6", "House 7", "House 8", "House 9", "House 10", "House 11", "House 12", "House 13", "House 14", "House 15", "House 16", "House 17", "House 18", "House 19", "House 20", "House 21", "House 22", "House 23", "House 24", "House 25", "House 26", "House 27", "House 28", "House 29", "House 30", "House 31", "House 32", "House 33", "House 34", "House 35", "House 36", "House 37"},
    Callback = function(value)
        selectedHouse = tonumber(string.match(value, "%d+"))
    end    
})
PermissionTab:AddButton({
    Name = "Grant Permission",
    Callback = function()
        GrantPermission(selectedHouse)
    end
})
-- Aba de Teleporte
local TeleportTab = Window:MakeTab({
    Name = "Teleport",
    Icon = "rbxassetid://4483362458",
    PremiumOnly = false
})

-- Seção para Teleportar para Players
TeleportTab:AddSection({
    Name = "Select Player"
})
local selectedPlayer = ""
local playerDropdown = TeleportTab:AddDropdown({
    Name = "Choose Player",
    Options = {},
    Callback = function(value)
        selectedPlayer = value
    end
})

-- Função para atualizar a lista de players dinamicamente
local function UpdatePlayerList()
    local players = game:GetService("Players"):GetPlayers()
    local playerNames = {}
    for _, player in ipairs(players) do
        table.insert(playerNames, player.Name)
    end
    playerDropdown:Refresh(playerNames, true)
    if #playerNames > 0 then
        selectedPlayer = playerNames[1]
    end
end

-- Atualizar a lista de players dinamicamente quando players entram ou saem
game:GetService("Players").PlayerAdded:Connect(UpdatePlayerList)
game:GetService("Players").PlayerRemoving:Connect(UpdatePlayerList)
UpdatePlayerList()

-- Adicionando um Botão para Teleportar para o Player Selecionado
TeleportTab:AddButton({
    Name = "Teleport",
    Callback = function()
        TeleportToPlayer(selectedPlayer)
    end
})

-- Adicionando um Botão para Assistir o Player Selecionado
TeleportTab:AddButton({
    Name = "Spectate",
    Callback = function()
        SpectatePlayer(selectedPlayer)
    end
})

-- Adicionando um Botão para Parar de Assistir
TeleportTab:AddButton({
    Name = "Stop Spectating",
    Callback = function()
        StopSpectating()
    end
})

-- Adicionando um Botão para Atualizar a Lista de Players
TeleportTab:AddButton({
    Name = "Refresh Player List",
    Callback = function()
        UpdatePlayerList()
    end
})

-- Aba de Name RP
local NameRPtab = Window:MakeTab({
    Name = "Name RP",
    Icon = "rbxassetid://4483362458",
    PremiumOnly = false
})

-- Seção para definir o Name RP
NameRPtab:AddSection({
    Name = "Set Name RP"
})

local newNameRP = ""
NameRPtab:AddTextbox({
    Name = "Enter RP Name",
    Default = "VitinHub",
    TextDisappear = true,
    Callback = function(value)
        newNameRP = value
    end
})

NameRPtab:AddButton({
    Name = "Set Name RP",
    Callback = function()
        ChangeNameRP(newNameRP)
    end
})

-- Seção para definir a cor do Name RP
NameRPtab:AddSection({
    Name = "Set Name RP Color"
})

local selectedColor = Color3.new(1, 1, 1) -- Cor branca por padrão
NameRPtab:AddColorPicker({
    Name = "Choose Name RP Color",
    Default = selectedColor,
    Callback = function(color)
        selectedColor = color
        ChangeNameColorRP(selectedColor)
    end
})
