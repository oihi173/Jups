local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

-- Função para criar explosão visual (efeito teológico)
local function createExplosion(parent)
    local explosion = Instance.new("Frame")
    explosion.Size = UDim2.new(0, math.random(40,80), 0, math.random(40,80))
    explosion.Position = UDim2.new(math.random(), 0, math.random(), 0)
    explosion.BackgroundColor3 = Color3.fromRGB(math.random(100,255), math.random(100,255), math.random(100,255))
    explosion.BackgroundTransparency = 0.3
    explosion.BorderSizePixel = 0
    explosion.Visible = true
    explosion.ZIndex = 10
    explosion.Parent = parent

    local tween = TweenService:Create(explosion, TweenInfo.new(0.7), {BackgroundTransparency = 1, Size = UDim2.new(0, 0, 0, 0)})
    tween:Play()
    tween.Completed:Connect(function()
        explosion:Destroy()
    end)
end

-- Criação do painel principal
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.Name = "TheologyMurderPanel"

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 380, 0, 340)
mainFrame.Position = UDim2.new(0.5, -190, 0.5, -170)
mainFrame.BackgroundColor3 = Color3.fromRGB(34, 34, 34)
mainFrame.BorderSizePixel = 0
mainFrame.Visible = false
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = ScreenGui

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 36)
title.BackgroundTransparency = 1
title.Text = "☦ Painel Teológico do Murder Mystery"
title.TextColor3 = Color3.fromRGB(200, 200, 0)
title.Font = Enum.Font.GothamBold
title.TextSize = 22
title.Parent = mainFrame

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 40, 0, 26)
closeBtn.Position = UDim2.new(1, -45, 0, 5)
closeBtn.Text = "✕"
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 19
closeBtn.BackgroundColor3 = Color3.fromRGB(220, 50, 50)
closeBtn.TextColor3 = Color3.fromRGB(255,255,255)
closeBtn.Parent = mainFrame

local openBtn = Instance.new("TextButton")
openBtn.Size = UDim2.new(0, 120, 0, 40)
openBtn.Position = UDim2.new(0.5, -60, 0.9, 0)
openBtn.Text = "ABRIR PAINEL"
openBtn.Font = Enum.Font.GothamBold
openBtn.TextSize = 20
openBtn.BackgroundColor3 = Color3.fromRGB(30, 180, 90)
openBtn.TextColor3 = Color3.fromRGB(255,255,255)
openBtn.Parent = ScreenGui

-- Efeito de explosão teológica ao abrir
openBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = true
    openBtn.Visible = false

    local t = tick()
    while tick() - t < 7 do
        createExplosion(ScreenGui)
        RunService.RenderStepped:Wait()
        if math.random() > 0.8 then
            createExplosion(ScreenGui)
        end
    end
end)

closeBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = false
    openBtn.Visible = true
end)

-- Murder Mystery Section
local murderLabel = Instance.new("TextLabel")
murderLabel.Size = UDim2.new(1, -20, 0, 28)
murderLabel.Position = UDim2.new(0, 10, 0, 44)
murderLabel.BackgroundTransparency = 1
murderLabel.Text = "⚔ Murder Mystery"
murderLabel.TextColor3 = Color3.fromRGB(255, 180, 60)
murderLabel.Font = Enum.Font.GothamBold
murderLabel.TextSize = 18
murderLabel.Parent = mainFrame

-- ESP Options
local espFrame = Instance.new("Frame")
espFrame.Size = UDim2.new(1, -20, 0, 98)
espFrame.Position = UDim2.new(0, 10, 0, 76)
espFrame.BackgroundTransparency = 0.6
espFrame.BackgroundColor3 = Color3.fromRGB(44,44,44)
espFrame.BorderSizePixel = 0
espFrame.Parent = mainFrame

local function addToggle(name, y, callback)
    local toggle = Instance.new("TextButton")
    toggle.Size = UDim2.new(0, 140, 0, 28)
    toggle.Position = UDim2.new(0, 16, 0, y)
    toggle.Text = "[ ] "..name
    toggle.Font = Enum.Font.Gotham
    toggle.TextSize = 15
    toggle.BackgroundColor3 = Color3.fromRGB(60,60,60)
    toggle.TextColor3 = Color3.fromRGB(200,200,200)
    toggle.Parent = espFrame

    local active = false
    toggle.MouseButton1Click:Connect(function()
        active = not active
        toggle.Text = active and "[✔] "..name or "[ ] "..name
        callback(active)
    end)
end

-- ESP Functions (implementação básica)
local function highlightRole(roleColor)
    for _, p in pairs(Players:GetPlayers()) do
        if p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
            local adorn = Instance.new("BoxHandleAdornment")
            adorn.Size = Vector3.new(3, 6, 3)
            adorn.Color3 = roleColor
            adorn.Transparency = 0.4
            adorn.ZIndex = 10
            adorn.Adornee = p.Character.HumanoidRootPart
            adorn.AlwaysOnTop = true
            adorn.Parent = ScreenGui
            delay(7, function() adorn:Destroy() end)
        end
    end
end

addToggle("ESP Assassino", 5, function(on)
    if on then highlightRole(Color3.fromRGB(220,0,0)) end
end)
addToggle("ESP Xerife", 38, function(on)
    if on then highlightRole(Color3.fromRGB(0,0,220)) end
end)
addToggle("ESP Inocente", 71, function(on)
    if on then highlightRole(Color3.fromRGB(0,220,0)) end
end)

-- Funções de noclip/fly/view
local actionFrame = Instance.new("Frame")
actionFrame.Size = UDim2.new(1, -20, 0, 120)
actionFrame.Position = UDim2.new(0, 10, 0, 184)
actionFrame.BackgroundTransparency = 0.6
actionFrame.BackgroundColor3 = Color3.fromRGB(44,44,44)
actionFrame.BorderSizePixel = 0
actionFrame.Parent = mainFrame

local function addActionBtn(name, y, callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 120, 0, 28)
    btn.Position = UDim2.new(0, 16, 0, y)
    btn.Text = name
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 15
    btn.BackgroundColor3 = Color3.fromRGB(60,60,60)
    btn.TextColor3 = Color3.fromRGB(200,200,200)
    btn.Parent = actionFrame
    btn.MouseButton1Click:Connect(callback)
end

local noclipActive = false
addActionBtn("Noclip", 5, function()
    noclipActive = true
end)
addActionBtn("UnNoclip", 38, function()
    noclipActive = false
end)

local flyActive = false
addActionBtn("Fly", 71, function()
    flyActive = true
end)
addActionBtn("UnFly", 104, function()
    flyActive = false
end)

-- Noclip e Fly Loop
RunService.Stepped:Connect(function()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        if noclipActive then
            for _,v in pairs(LocalPlayer.Character:GetDescendants()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end
            end
        else
            for _,v in pairs(LocalPlayer.Character:GetDescendants()) do
                if v:IsA("BasePart") then
                    v.CanCollide = true
                end
            end
        end
        if flyActive then
            LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(0,20,0)
        end
    end
end)

-- View/UnView Jogando (Selecionar player para assistir)
local viewPlayersFrame = Instance.new("Frame")
viewPlayersFrame.Size = UDim2.new(0, 108, 0, 120)
viewPlayersFrame.Position = UDim2.new(1, -118, 0, 184)
viewPlayersFrame.BackgroundTransparency = 0.8
viewPlayersFrame.BackgroundColor3 = Color3.fromRGB(34,34,34)
viewPlayersFrame.BorderSizePixel = 0
viewPlayersFrame.Parent = mainFrame

local viewing = nil

local function updatePlayersList()
    for _, child in pairs(viewPlayersFrame:GetChildren()) do
        if child:IsA("TextButton") then child:Destroy() end
    end
    local y = 4
    for _,p in ipairs(Players:GetPlayers()) do
        if p ~= LocalPlayer then
            local btn = Instance.new("TextButton")
            btn.Size = UDim2.new(1, -10, 0, 24)
            btn.Position = UDim2.new(0, 5, 0, y)
            btn.Text = "View "..p.Name
            btn.Font = Enum.Font.Gotham
            btn.TextSize = 13
            btn.BackgroundColor3 = Color3.fromRGB(50,50,50)
            btn.TextColor3 = Color3.fromRGB(240,240,240)
            btn.Parent = viewPlayersFrame
            btn.MouseButton1Click:Connect(function()
                workspace.CurrentCamera.CameraSubject = p.Character and p.Character:FindFirstChild("Humanoid") or p.Character
                viewing = p
            end)
            y = y + 26
        end
    end
    -- Unview
    local unBtn = Instance.new("TextButton")
    unBtn.Size = UDim2.new(1, -10, 0, 24)
    unBtn.Position = UDim2.new(0, 5, 0, y)
    unBtn.Text = "UnView"
    unBtn.Font = Enum.Font.Gotham
    unBtn.TextSize = 13
    unBtn.BackgroundColor3 = Color3.fromRGB(220,80,80)
    unBtn.TextColor3 = Color3.fromRGB(255,255,255)
    unBtn.Parent = viewPlayersFrame
    unBtn.MouseButton1Click:Connect(function()
        workspace.CurrentCamera.CameraSubject = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") or LocalPlayer.Character
        viewing = nil
    end)
end

updatePlayersList()
Players.PlayerAdded:Connect(updatePlayersList)
Players.PlayerRemoving:Connect(updatePlayersList)

-- O painel pode ser movido, aberto/fechado, e está organizado
-- Adicione funções de detecção de papéis do Murder Mystery para ESP se necessário (depende do jogo)

-- FIM DO SCRIPT
