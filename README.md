local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

--// Variáveis
local painelAberto = false
local flyAtivo = false
local noclipAtivo = false
local giantAtivo = false
local conexoes = {}
local esps = {}

--// UI
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "PainelMM2_" .. math.random(1000,9999)

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0,350,0,420)
MainFrame.Position = UDim2.new(0.5,-175,0.5,-210)
MainFrame.BackgroundColor3 = Color3.fromRGB(35,35,43)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Visible = false
MainFrame.BorderSizePixel = 0

local Title = Instance.new("TextLabel", MainFrame)
Title.Size = UDim2.new(1,0,0,35)
Title.BackgroundTransparency = 1
Title.Text = "tst 0.1 | Painel MM2"
Title.Font = Enum.Font.GothamBold
Title.TextColor3 = Color3.fromRGB(255,255,255)
Title.TextSize = 20

local ToggleButton = Instance.new("TextButton", ScreenGui)
ToggleButton.Size = UDim2.new(0,50,0,50)
ToggleButton.Position = UDim2.new(0,15,0.5,-25)
ToggleButton.BackgroundColor3 = Color3.fromRGB(45,45,55)
ToggleButton.Text = "≡"
ToggleButton.TextSize = 30
ToggleButton.Font = Enum.Font.GothamBlack
ToggleButton.TextColor3 = Color3.fromRGB(255,255,255)
ToggleButton.AutoButtonColor = false
ToggleButton.Draggable = true

local Y = 45
function addButton(text, callback)
    local btn = Instance.new("TextButton", MainFrame)
    btn.Size = UDim2.new(1,-20,0,35)
    btn.Position = UDim2.new(0,10,0, Y)
    btn.BackgroundColor3 = Color3.fromRGB(55,55,70)
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.Font = Enum.Font.Gotham
    btn.Text = text
    btn.TextSize = 18
    btn.AutoButtonColor = true
    btn.MouseButton1Click:Connect(callback)
    Y = Y + 40
    return btn
end

--// Funções

-- Contagem 7 segundos ao abrir
for i = 0,7 do
    Title.Text = "tst 0.1 | Painel MM2 • "..i
    wait(1)
end
Title.Text = "tst 0.1 | Painel MM2"

-- Toggle Painel
ToggleButton.MouseButton1Click:Connect(function()
    painelAberto = not painelAberto
    MainFrame.Visible = painelAberto
end)

--// ESP
