local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "CustomPanel"
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 400, 0, 320)
MainFrame.Position = UDim2.new(0.5, -200, 0.5, -160)
MainFrame.BackgroundColor3 = Color3.fromRGB(32, 32, 32)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

-- Botão fechar
local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 0, 5)
CloseButton.Text = "X"
CloseButton.BackgroundColor3 = Color3.fromRGB(200, 60, 60)
CloseButton.TextColor3 = Color3.new(1,1,1)
CloseButton.Parent = MainFrame

-- Botão abrir (invisível até fechar)
local OpenButton = Instance.new("TextButton")
OpenButton.Size = UDim2.new(0, 60, 0, 30)
OpenButton.Position = UDim2.new(0, 10, 0, 10)
OpenButton.Text = "Abrir"
OpenButton.Visible = false
OpenButton.Parent = ScreenGui

-- Título
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -40, 0, 30)
Title.Position = UDim2.new(0, 10, 0, 5)
Title.BackgroundTransparency = 1
Title.Text = "Painel Roblox"
Title.TextSize = 22
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.SourceSansBold
Title.Parent = MainFrame

-- Guia de URL
local UrlLabel = Instance.new("TextLabel")
UrlLabel.Text = "Coloque o link/URL:"
UrlLabel.Size = UDim2.new(0, 200, 0, 20)
UrlLabel.Position = UDim2.new(0, 10, 0, 45)
UrlLabel.BackgroundTransparency = 1
UrlLabel.TextColor3 = Color3.new(1,1,1)
UrlLabel.Parent = MainFrame

local UrlBox = Instance.new("TextBox")
UrlBox.Size = UDim2.new(0, 240, 0, 25)
UrlBox.Position = UDim2.new(0, 10, 0, 65)
UrlBox.PlaceholderText = "Cole aqui o link para usar..."
UrlBox.BackgroundColor3 = Color3.fromRGB(40,40,40)
UrlBox.TextColor3 = Color3.new(1,1,1)
UrlBox.Parent = MainFrame

-- Área para colocar coisas dentro do Roblox (pode ser script, asset, etc.)
local ContentLabel = Instance.new("TextLabel")
ContentLabel.Text = "Conteúdo:"
ContentLabel.Size = UDim2.new(0, 200, 0, 20)
ContentLabel.Position = UDim2.new(0, 10, 0, 100)
ContentLabel.BackgroundTransparency = 1
ContentLabel.TextColor3 = Color3.new(1,1,1)
ContentLabel.Parent = MainFrame

local ContentBox = Instance.new("TextBox")
ContentBox.Size = UDim2.new(0, 240, 0, 60)
ContentBox.Position = UDim2.new(0, 10, 0, 120)
ContentBox.PlaceholderText = "Coloque aqui o que quiser inserir no jogo..."
ContentBox.BackgroundColor3 = Color3.fromRGB(40,40,40)
ContentBox.TextColor3 = Color3.new(1,1,1)
ContentBox.TextWrapped = true
ContentBox.TextYAlignment = Enum.TextYAlignment.Top
ContentBox.ClearTextOnFocus = false
ContentBox.Parent = MainFrame

-- Função de exemplo para mostrar ação ao clicar
local function Notify(msg)
    game.StarterGui:SetCore("SendNotification", {
        Title = "Painel Roblox";
        Text = msg;
        Duration = 2;
    })
end

-- Botões de ações
local actions = {
    {Name="ESP",      Callback=function() Notify("ESP Ativado (exemplo)") end},
    {Name="UNESP",    Callback=function() Notify("ESP Desativado (exemplo)") end},
    {Name="VIEW",     Callback=function() Notify("View ativada (exemplo)") end},
    {Name="JOGANDO",  Callback=function() Notify("Jogando...") end},
    {Name="SPIN",     Callback=function() Notify("Spin ativado (exemplo)") end},
    {Name="UNSPIN",   Callback=function() Notify("Spin desativado (exemplo)") end},
    {Name="FLING",    Callback=function() Notify("Fling ativado (exemplo)") end},
    {Name="UNFLING",  Callback=function() Notify("Fling desativado (exemplo)") end}
}

for i, info in ipairs(actions) do
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 90, 0, 30)
    btn.Position = UDim2.new(0, 270 + ((i-1)%2)*100, 0, 45 + math.floor((i-1)/2)*40)
    btn.Text = info.Name
    btn.BackgroundColor3 = Color3.fromRGB(60, 60, 120)
    btn.TextColor3 = Color3.new(1,1,1)
    btn.Parent = MainFrame
    btn.MouseButton1Click:Connect(info.Callback)
end

-- Fechar painel
CloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
    OpenButton.Visible = true
end)
-- Abrir painel
OpenButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
    OpenButton.Visible = false
end)

-- Deixar painel sempre em cima (opcional)
MainFrame.ZIndex = 10
OpenButton.ZIndex = 11

-- Dica: para funcionalidades ESP, Fling, etc. você deve integrar scripts/exploits próprios no callback de cada botão.

-- Pronto! O painel está criado e funcional.
