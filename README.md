--[[  
MultiGame ESP + Panel
---------------------
- Murder Mystery 2: ESP cores (azul/xerife, vermelho/assassino, verde/inocente)
- Grow a Garden: ESP frutas
- Doors: ESP portas
- Blade Ball: auto repartir bola
- Painel: Fly/Unfly, ViewPlayer/Unview, Noclip/Unnoclip, Raio-X/Unraio-X
]]

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("MultiGame ESP Panel", "DarkTheme")

local murderTab = Window:NewTab("Murder Mystery ESP")
local gardenTab = Window:NewTab("Grow a Garden ESP")
local doorsTab = Window:NewTab("Doors ESP")
local bladeTab = Window:NewTab("Blade Ball")
local miscTab = Window:NewTab("Funções Extras")

-- Helper ESP function
local function createESP(obj, color)
    if obj:FindFirstChild("ESP") then return end
    local espBox = Instance.new("BoxHandleAdornment", obj)
    espBox.Name = "ESP"
    espBox.Adornee = obj
    espBox.Size = obj.Size
    espBox.Color3 = color
    espBox.AlwaysOnTop = true
    espBox.ZIndex = 10
    espBox.Transparency = 0.5
end

-- Murder Mystery ESP
murderTab:NewButton("Ativar ESP (Cores)", "ESP xerife, assassino, inocente", function()
    for _,v in pairs(game.Players:GetPlayers()) do
        if v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
            -- Detectar função do jogador (exemplo, adapte ao MM2 real)
            local role = v:GetAttribute("Role") or "Inocente"
            if role == "Xerife" then
                createESP(v.Character.HumanoidRootPart, Color3.fromRGB(0, 150, 255)) -- Azul
            elseif role == "Assassino" then
                createESP(v.Character.HumanoidRootPart, Color3.fromRGB(255, 50, 50)) -- Vermelho
            else
                createESP(v.Character.HumanoidRootPart, Color3.fromRGB(80, 255, 80)) -- Verde
            end
        end
    end
end)

-- Grow a Garden ESP
gardenTab:NewButton("Ativar ESP Frutas", "Destaca todas frutas", function()
    for _,obj in pairs(workspace:GetChildren()) do
        if obj:IsA("Part") and obj.Name:lower():find("fruta") then
            createESP(obj, Color3.fromRGB(255, 220, 0))
        end
    end
end)

-- Doors ESP
doorsTab:NewButton("Ativar ESP Portas", "Destaca porta", function()
    for _,obj in pairs(workspace:GetChildren()) do
        if obj:IsA("Part") and obj.Name:lower():find("door") then
            createESP(obj, Color3.fromRGB(120, 120, 255))
        end
    end
end)

-- Blade Ball Auto Repartir Bola
bladeTab:NewToggle("Auto repartir bola", "Reparte a bola automaticamente", function(state)
    getgenv().AutoSplit = state
    spawn(function()
        while getgenv().AutoSplit do
            -- Exemplo: Chame a função do Blade Ball, adapte ao jogo original
            local ball = workspace:FindFirstChild("Ball")
            if ball then
                game:GetService("ReplicatedStorage"):WaitForChild("SplitBallEvent"):FireServer(ball)
            end
            wait(0.5)
        end
    end)
end)

-- Funções Extras
miscTab:NewButton("Fly", "Ativa fly", function()
    loadstring(game:HttpGet("https://pastebin.com/raw/6b7yYVYv"))() -- Script fly genérico
end)
miscTab:NewButton("Unfly", "Desativa fly", function()
    -- Geralmente basta desativar o script de fly
    pcall(function() shared.FlyEnabled = false end)
end)
miscTab:NewTextBox("View Player", "Digite nome para view", function(txt)
    local plr = game.Players:FindFirstChild(txt)
    if plr and plr.Character then
        workspace.CurrentCamera.CameraSubject = plr.Character.Humanoid
    end
end)
miscTab:NewButton("Unview", "Volta visão para você", function()
    local me = game.Players.LocalPlayer
    workspace.CurrentCamera.CameraSubject = me.Character.Humanoid
end)
miscTab:NewButton("Noclip", "Ativa noclip", function()
    getgenv().noclip = true
    game:GetService("RunService").Stepped:Connect(function()
        if getgenv().noclip then
            for _,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end
            end
        end
    end)
end)
miscTab:NewButton("Unnoclip", "Desativa noclip", function()
    getgenv().noclip = false
    for _,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
        if v:IsA("BasePart") then
            v.CanCollide = true
        end
    end
end)
miscTab:NewButton("Raio-X", "Ativa raio-x", function()
    for _,v in pairs(workspace:GetDescendants()) do
        if v:IsA("BasePart") then
            v.Transparency = 0.5
        end
    end
end)
miscTab:NewButton("Unraio-X", "Desativa raio-x", function()
    for _,v in pairs(workspace:GetDescendants()) do
        if v:IsA("BasePart") then
            v.Transparency = 0
        end
    end
end)

-- Aviso
Library:Notification("MultiGame ESP Panel", "Algumas funções podem precisar de ajustes para jogos diferentes!", 5)
