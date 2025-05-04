-- Jamba Hub (corrigido para exibir corretamente no PlayerGui)

local player = game:GetService("Players").LocalPlayer
local gui = player:WaitForChild("PlayerGui")

-- Remove se já existir
if gui:FindFirstChild("JambaHub") then
    gui.JambaHub:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local CloseButton = Instance.new("TextButton")
local SideMenu = Instance.new("Frame")
local TabsFrame = Instance.new("Frame")

local tabs = {
    "MAIN", "PLAYER", "VISUALS", "ANIMATION", "EMOTE", "SUS", "TROLLS"
}

local tabButtons = {}
local tabFrames = {}
local activeTab = nil

-- Setup GUI
ScreenGui.Name = "JambaHub"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = gui

MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
MainFrame.BorderSizePixel = 0
MainFrame.Position = UDim2.new(0.3, 0, 0.2, 0)
MainFrame.Size = UDim2.new(0, 500, 0, 300)
MainFrame.Active = true
MainFrame.Draggable = true

Title.Name = "Title"
Title.Parent = MainFrame
Title.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Text = "Jamba Hub"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 20

CloseButton.Name = "CloseButton"
CloseButton.Parent = MainFrame
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -30, 0, 0)
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.new(1, 1, 1)
CloseButton.Font = Enum.Font.SourceSansBold
CloseButton.TextSize = 18
CloseButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)

SideMenu.Name = "SideMenu"
SideMenu.Parent = MainFrame
SideMenu.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
SideMenu.Size = UDim2.new(0, 120, 1, -30)
SideMenu.Position = UDim2.new(0, 0, 0, 30)

TabsFrame.Name = "TabsFrame"
TabsFrame.Parent = MainFrame
TabsFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
TabsFrame.Position = UDim2.new(0, 120, 0, 30)
TabsFrame.Size = UDim2.new(1, -120, 1, -30)

-- Criar abas
for i, tabName in ipairs(tabs) do
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, 0, 0, 35)
    btn.Position = UDim2.new(0, 0, 0, (i - 1) * 35)
    btn.Text = tabName
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.Font = Enum.Font.SourceSans
    btn.TextSize = 16
    btn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    btn.Parent = SideMenu
    tabButtons[tabName] = btn

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 1, 0)
    frame.BackgroundTransparency = 1
    frame.Visible = false
    frame.Parent = TabsFrame
    tabFrames[tabName] = frame

    btn.MouseButton1Click:Connect(function()
        if activeTab then
            tabFrames[activeTab].Visible = false
        end
        activeTab = tabName
        tabFrames[activeTab].Visible = true
    end)
end

-- Ativar aba VISUALS por padrão
tabFrames["VISUALS"].Visible = true
activeTab = "VISUALS"

-- Exemplo: botão de ativar ESP
local toggleESP = Instance.new("TextButton")
toggleESP.Size = UDim2.new(0, 150, 0, 40)
toggleESP.Position = UDim2.new(0, 20, 0, 20)
toggleESP.Text = "ESP OFF"
toggleESP.TextColor3 = Color3.new(1, 1, 1)
toggleESP.Font = Enum.Font.SourceSansBold
toggleESP.TextSize = 18
toggleESP.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
toggleESP.Parent = tabFrames["VISUALS"]

local espEnabled = false
toggleESP.MouseButton1Click:Connect(function()
    espEnabled = not espEnabled
    toggleESP.Text = espEnabled and "ESP ON" or "ESP OFF"
    -- Insira seu código de ESP aqui
end)

-- Fechar janela
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)
