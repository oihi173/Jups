local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer

-- Funções auxiliares
local function createBillboard(player, color)
    if player.Character and not player.Character:FindFirstChild("ESPBill") then
        local head = player.Character:FindFirstChild("Head")
        if head then
            local bill = Instance.new("BillboardGui", head)
            bill.Name = "ESPBill"
            bill.Size = UDim2.new(0, 80, 0, 20)
            bill.AlwaysOnTop = true
            bill.Adornee = head
            local txt = Instance.new("TextLabel", bill)
            txt.Size = UDim2.new(1, 0, 1, 0)
            txt.Text = player.Name
            txt.BackgroundTransparency = 1
            txt.TextColor3 = color
            txt.Font = Enum.Font.Cartoon
            txt.TextScaled = true
        end
    end
end

local function removeBillboard(player)
    if player.Character and player.Character:FindFirstChild("ESPBill") then
        player.Character.ESPBill:Destroy()
    end
end

local espOn = false

local function enableESP()
    espOn = true
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            createBillboard(player, Color3.fromRGB(math.random(0,255), math.random(0,255), math.random(0,255)))
        end
    end
end

local function disableESP()
    espOn = false
    for _, player in pairs(Players:GetPlayers()) do
        removeBillboard(player)
    end
end

Players.PlayerAdded:Connect(function(p)
    if espOn then
        p.CharacterAdded:Connect(function()
            wait(0.5)
            createBillboard(p, Color3.fromRGB(math.random(0,255), math.random(0,255), math.random(0,255)))
        end)
    end
end)

-- Painel UI
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "PainelESP"

-- Epic face icon
local Epic = Instance.new("ImageLabel", ScreenGui)
Epic.Size = UDim2.new(0,100,0,100)
Epic.Position = UDim2.new(0,10,0,10)
Epic.BackgroundTransparency = 1
Epic.Image = "http://www.roblox.com/asset/?id=10907548" -- Epic Face

-- Painel Frame
local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 200, 0, 220)
Frame.Position = UDim2.new(0, 120, 0, 10)
Frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Frame.BackgroundTransparency = 0.15
Frame.BorderSizePixel = 2

-- Título
local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1,0,0,30)
Title.Text = "Painel ESP & Fling"
Title.TextColor3 = Color3.fromRGB(255,255,0)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.Cartoon
Title.TextScaled = true

-- Botões
local function createButton(txt, pos, callback)
    local btn = Instance.new("TextButton", Frame)
    btn.Size = UDim2.new(0.9, 0, 0, 35)
    btn.Position = UDim2.new(0.05, 0, 0, pos)
    btn.BackgroundColor3 = Color3.fromRGB(60,60,60)
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.Font = Enum.Font.Cartoon
    btn.Text = txt
    btn.TextScaled = true
    btn.MouseButton1Click:Connect(callback)
    return btn
end

createButton("ESP Colorido",40,function()
    enableESP()
end)

createButton("UnESP",80,function()
    disableESP()
end)

-- Fling All
local flinging = false
createButton("Fling All",120,function()
    flinging = true
    for _,plr in pairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
            spawn(function()
                while flinging and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") do
                    local hrp = plr.Character.HumanoidRootPart
                    hrp.Velocity = Vector3.new(9999,9999,9999)
                    wait(0.1)
                end
            end)
        end
    end
end)

-- UnFling
createButton("Unfling",160,function()
    flinging = false
    for _,plr in pairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
            plr.Character.HumanoidRootPart.Velocity = Vector3.new(0,0,0)
        end
    end
end)

-- Créditos
local credits = Instance.new("TextLabel", Frame)
credits.Size = UDim2.new(1,0,0,20)
credits.Position = UDim2.new(0,0,1,-20)
credits.Text = "By copilot | oihi173"
credits.TextColor3 = Color3.fromRGB(255,255,255)
credits.BackgroundTransparency = 1
credits.Font = Enum.Font.Cartoon
credits.TextScaled = true

-- Atalho para esconder/mostrar painel
local painelVis = true
game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.RightShift then
        painelVis = not painelVis
        Frame.Visible = painelVis
        Epic.Visible = painelVis
    end
end)
