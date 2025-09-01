
loadstring([[
local Players = game:GetService("Players")
local CollectionService = game:GetService("CollectionService")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "OIHI173HUB"
screenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

-- Criar painel principal
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 250, 0, 300)
frame.Position = UDim2.new(0.1, 0, 0.2, 0)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BackgroundTransparency = 0.2
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true
frame.Parent = screenGui

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundTransparency = 1
title.Text = "OIHI 173 HUB"
title.Font = Enum.Font.SourceSansBold
title.TextSize = 20
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Parent = frame

-- Botões de ESP
local options = {
    {"ESP Assassino", "Assassino", Color3.fromRGB(255,0,0)},
    {"ESP Xerife", "Xerife", Color3.fromRGB(0,0,255)},
    {"ESP Herói", "Heroi", Color3.fromRGB(255,255,0)},
    {"ESP Inocente", "Inocente", Color3.fromRGB(0,255,0)},
}

local toggles = {}

for i, data in ipairs(options) do
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 40)
    btn.Position = UDim2.new(0, 10, 0, 40 * i)
    btn.BackgroundColor3 = Color3.fromRGB(40,40,40)
    btn.Text = data[1].." [OFF]"
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 18
    btn.Parent = frame

    toggles[data[2]] = {enabled = false, button = btn, color = data[3]}

    btn.MouseButton1Click:Connect(function()
        toggles[data[2]].enabled = not toggles[data[2]].enabled
        if toggles[data[2]].enabled then
            btn.Text = data[1].." [ON]"
            btn.BackgroundColor3 = Color3.fromRGB(60,100,60)
        else
            btn.Text = data[1].." [OFF]"
            btn.BackgroundColor3 = Color3.fromRGB(40,40,40)
        end
    end)
end

-- Criar BillboardGui para jogadores
local function createBillboard(player, tag, color)
    if player.Character and player.Character:FindFirstChild("Head") then
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "RoleBillboard"
        billboard.Adornee = player.Character.Head
        billboard.Size = UDim2.new(0,100,0,30)
        billboard.AlwaysOnTop = true
        billboard.Parent = player.Character.Head

        local textLabel = Instance.new("TextLabel")
        textLabel.Size = UDim2.new(1,0,1,0)
        textLabel.BackgroundTransparency = 1
        textLabel.Text = tag
        textLabel.TextColor3 = color
        textLabel.Font = Enum.Font.SourceSansBold
        textLabel.TextSize = 16
        textLabel.Parent = billboard
    end
end

-- Loop de ESP
RunService.RenderStepped:Connect(function()
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Head") then
            local head = player.Character.Head
            local billboard = head:FindFirstChild("RoleBillboard")

            if billboard then
                billboard:Destroy()
            end

            for tag, data in pairs(toggles) do
                if data.enabled and CollectionService:HasTag(player, tag) then
                    createBillboard(player, tag, data.color)
                end
            end
        end
    end
end)
]])()
