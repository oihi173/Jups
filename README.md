local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local mouse = LocalPlayer:GetMouse()

local panel = Instance.new("ScreenGui")
panel.Name = "PainelCompleto"
panel.Parent = game:GetService("CoreGui")

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 350, 0, 530)
mainFrame.Position = UDim2.new(0.5, -175, 0.5, -265)
mainFrame.BackgroundTransparency = 1 -- Removido fundo preto
mainFrame.BorderSizePixel = 2
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = panel

local capa = Instance.new("TextLabel")
capa.Size = UDim2.new(1, 0, 0, 210)
capa.Position = UDim2.new(0,0,0,0)
capa.BackgroundTransparency = 1
capa.TextColor3 = Color3.fromRGB(200,255,200)
capa.Font = Enum.Font.Code
capa.TextSize = 16
capa.TextXAlignment = Enum.TextXAlignment.Left
capa.TextYAlignment = Enum.TextYAlignment.Top
capa.Text = [[⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⣠⣤⠶⠶⠶⠶⠶⢦⣤⣀⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⣠⡶⠛⠋⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠙⠛⢦⣄⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⣰⠞⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠉⠳⣄⠀⠀⠀⠀
⠀⠀⢠⡾⠁⠀⠀⢀⣤⣤⣤⣤⣄⠀⠀⠀⠀⠀⠀⠀⠀⣠⣤⣤⣤⡙⢷⡀⠀⠀
⠀⢠⡟⠀⠀⠀⣰⣿⣿⡇⠀⠀⠙⢷⡀⠀⠀⠀⠀⢠⣾⣿⣿⠀⠀⠹⣮⢿⡀⠀
⠀⣾⠀⠀⠀⢰⡏⠙⠛⠁⠀⠀⠀⠘⡇⠀⠀⠀⠀⣸⠋⠛⠋⠀⠀⠀⢹⠈⣧⠀
⢸⡇⠀⠀⠀⠘⣧⣤⣤⣤⣤⣤⣤⣤⡇⠀⠀⠀⠀⢸⣧⣤⣤⣤⣤⣤⣾⠀⢹⡆
⢸⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢸⡇
⢸⡇⠀⠀⠀⠀⣰⣶⣶⣶⣶⣶⣶⣶⣶⣶⣶⣶⣶⣶⣶⣶⣶⣶⡶⠀⠀⣸⠇
⠀⣿⠀⠀⠀⠀⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠁⠀⢀⡟⠀
⠀⠘⣧⠀⠀⠀⢻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠃⠀⠀⣾⠁⠀
⠀⠀⠘⢷⡀⠀⠀⢻⣿⡻⠋⠁⠀⠀⠀⠉⠻⣿⣿⣿⣿⡿⠃⠀⢠⡾⠁⠀⠀
⠀⠀⠀⠀⠻⣦⡀⠀⠙⠷⣤⣀⠀⠀⠀⠀⠀⠈⣿⣿⡿⠋⠀⣀⡴⠋⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠙⠷⣤⣀⠀⠉⠛⠓⠒⠒⠒⠚⠋⠁⣠⣤⠾⠋⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠉⠙⠛⠶⠶⠶⠶⠶⠶⠛⠋⠉⠀⠀⠀⠀⠀⠀⠀⠀⠀]]
capa.Parent = mainFrame

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 40, 0, 30)
closeBtn.Position = UDim2.new(1, -45, 0, 5)
closeBtn.Text = "✕"
closeBtn.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
closeBtn.TextColor3 = Color3.fromRGB(255,255,255)
closeBtn.Parent = mainFrame

local openBtn = Instance.new("TextButton")
openBtn.Size = UDim2.new(0, 60, 0, 30)
openBtn.Position = UDim2.new(0, 10, 1, -40)
openBtn.Text = "Abrir Painel"
openBtn.BackgroundColor3 = Color3.fromRGB(50, 200, 50)
openBtn.TextColor3 = Color3.fromRGB(255,255,255)
openBtn.Visible = false
openBtn.Parent = panel

local moveLeftBtn = Instance.new("TextButton")
moveLeftBtn.Size = UDim2.new(0, 40, 0, 30)
moveLeftBtn.Position = UDim2.new(0, 5, 0, 5)
moveLeftBtn.Text = "←"
moveLeftBtn.Parent = mainFrame

local moveRightBtn = Instance.new("TextButton")
moveRightBtn.Size = UDim2.new(0, 40, 0, 30)
moveRightBtn.Position = UDim2.new(0, 55, 0, 5)
moveRightBtn.Text = "→"
moveRightBtn.Parent = mainFrame

-- Dropdown para selecionar jogador
local viewDropdown = Instance.new("TextBox")
viewDropdown.Size = UDim2.new(0.8, 0, 0, 30)
viewDropdown.Position = UDim2.new(0.1, 0, 0, 395)
viewDropdown.BackgroundColor3 = Color3.fromRGB(45,45,45)
viewDropdown.PlaceholderText = "Nome do jogador para View"
viewDropdown.TextColor3 = Color3.fromRGB(255,255,255)
viewDropdown.Font = Enum.Font.GothamBold
viewDropdown.TextSize = 16
viewDropdown.Parent = mainFrame

-- Botão utilitário
local function createButton(text, posY)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.8, 0, 0, 30)
    btn.Position = UDim2.new(0.1, 0, 0, posY)
    btn.BackgroundColor3 = Color3.fromRGB(40, 40, 60)
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.Text = text
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 16
    btn.Parent = mainFrame
    return btn
end

local btnEsp = createButton("ESP", 220)
local btnUnEsp = createButton("UnESP", 255)
local btnFly = createButton("Fly (ADM)", 290)
local btnUnFly = createButton("UnFly", 325)
local btnNoclip = createButton("Noclip", 360)
local btnUnNoclip = createButton("UnNoclip", 395)
local btnView = createButton("Ver Jogador", 430)
local btnUnView = createButton("UnView", 465)
local btnFling = createButton("Fling Player", 500)
local btnUnFling = createButton("UnFling Player", 535)
local btnIA = createButton("IA Movement", 570)

-- Fechar/Abrir Painel
closeBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = false
    openBtn.Visible = true
end)
openBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = true
    openBtn.Visible = false
end)

-- Mover para os lados
moveLeftBtn.MouseButton1Click:Connect(function()
    local pos = mainFrame.Position
    mainFrame.Position = UDim2.new(pos.X.Scale, pos.X.Offset-50, pos.Y.Scale, pos.Y.Offset)
end)
moveRightBtn.MouseButton1Click:Connect(function()
    local pos = mainFrame.Position
    mainFrame.Position = UDim2.new(pos.X.Scale, pos.X.Offset+50, pos.Y.Scale, pos.Y.Offset)
end)

-- ESP
local espOn = false
btnEsp.MouseButton1Click:Connect(function()
    espOn = true
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= LocalPlayer and p.Character and p.Character:FindFirstChild("Head") then
            if not p.Character.Head:FindFirstChild("ESP") then
                local billboard = Instance.new("BillboardGui")
                billboard.Name = "ESP"
                billboard.Adornee = p.Character.Head
                billboard.Size = UDim2.new(0, 100, 0, 40)
                billboard.AlwaysOnTop = true
                billboard.Parent = p.Character.Head
                local label = Instance.new("TextLabel")
                label.Size = UDim2.new(1,0,1,0)
                label.BackgroundTransparency = 1
                label.Text = p.Name
                label.TextColor3 = Color3.fromRGB(255,50,50)
                label.TextScaled = true
                label.Parent = billboard
            end
        end
    end
end)
btnUnEsp.MouseButton1Click:Connect(function()
    espOn = false
    for _, p in pairs(Players:GetPlayers()) do
        if p.Character and p.Character:FindFirstChild("Head") then
            local esp = p.Character.Head:FindFirstChild("ESP")
            if esp then esp:Destroy() end
        end
    end
end)

-- Fly (ADM estilo)
local flying = false
local flyConn
local flyVel
btnFly.MouseButton1Click:Connect(function()
    if flying then return end
    flying = true
    local char = LocalPlayer.Character
    if not char or not char:FindFirstChild("HumanoidRootPart") then return end
    flyVel = Instance.new("BodyVelocity")
    flyVel.MaxForce = Vector3.new(1e5,1e5,1e5)
    flyVel.Velocity = Vector3.new(0,0,0)
    flyVel.Parent = char.HumanoidRootPart

    local function getFlyVector()
        local v = Vector3.new()
        if UserInputService:IsKeyDown(Enum.KeyCode.W) then v = v + workspace.CurrentCamera.CFrame.LookVector end
        if UserInputService:IsKeyDown(Enum.KeyCode.S) then v = v - workspace.CurrentCamera.CFrame.LookVector end
        if UserInputService:IsKeyDown(Enum.KeyCode.A) then v = v - workspace.CurrentCamera.CFrame.RightVector end
        if UserInputService:IsKeyDown(Enum.KeyCode.D) then v = v + workspace.CurrentCamera.CFrame.RightVector end
        if UserInputService:IsKeyDown(Enum.KeyCode.Space) then v = v + Vector3.new(0,1,0) end
        if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then v = v - Vector3.new(0,1,0) end
        return v.Unit * 60
    end

    local UserInputService = game:GetService("UserInputService")
    flyConn = game:GetService("RunService").Heartbeat:Connect(function()
        if char and char:FindFirstChild("HumanoidRootPart") and flying then
            flyVel.Velocity = getFlyVector()
        end
    end)
end)
btnUnFly.MouseButton1Click:Connect(function()
    flying = false
    if flyConn then flyConn:Disconnect() end
    local char = LocalPlayer.Character
    if char and char:FindFirstChild("HumanoidRootPart") and flyVel then
        flyVel:Destroy()
    end
end)

-- Noclip
local noclipActive = false
local noclipConn
btnNoclip.MouseButton1Click:Connect(function()
    if noclipActive then return end
    noclipActive = true
    noclipConn = game:GetService("RunService").Stepped:Connect(function()
        local char = LocalPlayer.Character
        if char then
            for _, part in pairs(char:GetDescendants()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end
    end)
end)
btnUnNoclip.MouseButton1Click:Connect(function()
    noclipActive = false
    if noclipConn then noclipConn:Disconnect() end
    local char = LocalPlayer.Character
    if char then
        for _, part in pairs(char:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
            end
        end
    end
end)

-- View Player (dropdown escolha)
local viewing = false
local origCam
btnView.MouseButton1Click:Connect(function()
    local name = viewDropdown.Text
    local target
    for _, p in ipairs(Players:GetPlayers()) do
        if p.Name:lower() == name:lower() then
            target = p
            break
        end
    end
    if not target or not target.Character or not target.Character:FindFirstChild("Head") then return end
    origCam = workspace.CurrentCamera.CameraSubject
    workspace.CurrentCamera.CameraSubject = target.Character.Head
    viewing = true
end)
btnUnView.MouseButton1Click:Connect(function()
    if viewing and origCam then
        workspace.CurrentCamera.CameraSubject = origCam
        viewing = false
    end
end)

-- Fling Player
local flinging = false
local flingConn
btnFling.MouseButton1Click:Connect(function()
    local name = viewDropdown.Text
    local target
    for _, p in ipairs(Players:GetPlayers()) do
        if p.Name:lower() == name:lower() then
            target = p
            break
        end
    end
    if not target or not target.Character or not target.Character:FindFirstChild("HumanoidRootPart") then return end
    flinging = true
    flingConn = game:GetService("RunService").Stepped:Connect(function()
        target.Character.HumanoidRootPart.Velocity = Vector3.new(500, 500, 500)
    end)
end)
btnUnFling.MouseButton1Click:Connect(function()
    flinging = false
    if flingConn then flingConn:Disconnect() end
end)

-- IA Movement
local iaActive = false
local iaConn
btnIA.MouseButton1Click:Connect(function()
    iaActive = not iaActive
    btnIA.Text = iaActive and "Parar IA" or "IA Movement"
    if iaActive then
        local directions = {Vector3.new(1,0,0), Vector3.new(-1,0,0), Vector3.new(0,0,1), Vector3.new(0,0,-1)}
        iaConn = game:GetService("RunService").Heartbeat:Connect(function()
            local char = LocalPlayer.Character
            if char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
                local dir = directions[math.random(1,#directions)]
                char.Humanoid:Move(dir, true)
                if math.random(1,50) == 1 then
                    char.Humanoid.Jump = true
                end
            end
        end)
    else
        if iaConn then iaConn:Disconnect() end
        btnIA.Text = "IA Movement"
    end
end)
