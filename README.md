local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.ResetOnSpawn = false

local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")
local HttpService = game:GetService("HttpService")
local LocalPlayer = Players.LocalPlayer
local Camera = Workspace.CurrentCamera

local ToggleStates = {
	Aimbot = false,
	SilentAim = false,
	TeamAimbot = false,
	UniversalESP = false,
	Tracer = false,
	PlayerESP = false,
	TeamESP = false,
	Fly = false,
	Walkspeed = false,
	Jumppower = false,
	InfiniteJump = false,
	NoClip = false,
	VehicleFly = false,
}

local AimbotConfig = {
	TargetPart = "Head",
	TargetTeam = "",
	FOVRadius = 150,
}

local ESPConfig = {
	TargetTeam = "",
}

local PlayerESPFilter = ""

local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.Active = true
MainFrame.BackgroundColor3 = Color3.fromRGB(49, 49, 49)
MainFrame.BorderColor3 = Color3.fromRGB(225, 194, 72)
MainFrame.BorderSizePixel = 0
MainFrame.Position = UDim2.new(0.264584661, 73, 0.1289507, 4)
MainFrame.Size = UDim2.new(0, 442, 0, 383)
MainFrame.ZIndex = 100
MainFrame.Draggable = false

local MainBorder = Instance.new("UIStroke")
MainBorder.Parent = MainFrame
MainBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
MainBorder.Color = Color3.fromRGB(150, 190, 255)
MainBorder.Thickness = 1.8
MainBorder.Transparency = 0

local MainShadow = Instance.new("UIStroke")
MainShadow.Parent = MainFrame
MainShadow.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual
MainShadow.Color = Color3.fromRGB(0, 0, 0)
MainShadow.Thickness = 1
MainShadow.Transparency = 0

local DragArea = Instance.new("Frame")
DragArea.Name = "DragArea"
DragArea.Parent = MainFrame
DragArea.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
DragArea.BackgroundTransparency = 1
DragArea.BorderSizePixel = 0
DragArea.Size = UDim2.new(1, 0, 0, 38)
DragArea.Position = UDim2.new(0, 0, 0, 0)
DragArea.ZIndex = 200
DragArea.Active = true

local TitleLabel = Instance.new("TextLabel")
TitleLabel.Parent = MainFrame
TitleLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.BackgroundTransparency = 1.000
TitleLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
TitleLabel.BorderSizePixel = 0
TitleLabel.Position = UDim2.new(0.03, 0, 0, 0)
TitleLabel.Size = UDim2.new(0, 50, 0, 38)
TitleLabel.Font = Enum.Font.SourceSansBold
TitleLabel.Text = "Ketamine"
TitleLabel.TextColor3 = Color3.fromRGB(214, 214, 214)
TitleLabel.TextSize = 13.000
TitleLabel.ZIndex = 201

local TitleStroke = Instance.new("UIStroke")
TitleStroke.Parent = TitleLabel
TitleStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual
TitleStroke.Color = Color3.fromRGB(0, 0, 0)
TitleStroke.Thickness = 1
TitleStroke.Transparency = 0

local ContentContainer = Instance.new("Frame")
ContentContainer.Parent = MainFrame
ContentContainer.BackgroundColor3 = Color3.fromRGB(33, 33, 33)
ContentContainer.BorderColor3 = Color3.fromRGB(38, 38, 38)
ContentContainer.BorderSizePixel = 0
ContentContainer.Position = UDim2.new(0.0175741203, 0, 0.0992167071, 0)
ContentContainer.Size = UDim2.new(0, 426, 0, 335)

local ContainerBorder = Instance.new("UIStroke")
ContainerBorder.Parent = ContentContainer
ContainerBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
ContainerBorder.Color = Color3.fromRGB(75, 75, 75)
ContainerBorder.Thickness = 1
ContainerBorder.Transparency = 0

local TabIndicator = Instance.new("Frame")
TabIndicator.Name = "TabIndicator"
TabIndicator.Parent = ContentContainer
TabIndicator.BackgroundColor3 = Color3.fromRGB(49, 49, 49)
TabIndicator.BorderColor3 = Color3.fromRGB(0, 0, 0)
TabIndicator.BorderSizePixel = 0
TabIndicator.Position = UDim2.new(0.021, 0, 0.058, 0)
TabIndicator.Size = UDim2.new(0, 42, 0, 3)
TabIndicator.ZIndex = 6

local MainTabButton = Instance.new("TextButton")
MainTabButton.Name = "MainTabButton"
MainTabButton.Parent = ContentContainer
MainTabButton.BackgroundColor3 = Color3.fromRGB(48, 48, 48)
MainTabButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
MainTabButton.BorderSizePixel = 0
MainTabButton.Position = UDim2.new(0.0211267602, 0, 0.0249400157, 0)
MainTabButton.Size = UDim2.new(0, 42, 0, 13)
MainTabButton.ZIndex = 5
MainTabButton.Font = Enum.Font.SourceSansBold
MainTabButton.Text = "Main"
MainTabButton.TextColor3 = Color3.fromRGB(220, 220, 220)
MainTabButton.TextSize = 10.000

local MainTabStroke = Instance.new("UIStroke")
MainTabStroke.Parent = MainTabButton
MainTabStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
MainTabStroke.Color = Color3.fromRGB(75, 75, 75)
MainTabStroke.Thickness = 1
MainTabStroke.Transparency = 0

local MainContentPanel = Instance.new("Frame")
MainContentPanel.Name = "MainContentPanel"
MainContentPanel.Parent = ContentContainer
MainContentPanel.BackgroundColor3 = Color3.fromRGB(49, 49, 49)
MainContentPanel.BorderColor3 = Color3.fromRGB(0, 0, 0)
MainContentPanel.BorderSizePixel = 0
MainContentPanel.Position = UDim2.new(0.0211267602, 0, 0.0635157749, 0)
MainContentPanel.Size = UDim2.new(0, 407, 0, 303)
MainContentPanel.ZIndex = 4
MainContentPanel.Visible = true

local ContentPanelBorder = Instance.new("UIStroke")
ContentPanelBorder.Parent = MainContentPanel
ContentPanelBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
ContentPanelBorder.Color = Color3.fromRGB(75, 75, 75)
ContentPanelBorder.Thickness = 1
ContentPanelBorder.Transparency = 0

local SectionTitle = Instance.new("TextLabel")
SectionTitle.Parent = MainContentPanel
SectionTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
SectionTitle.BackgroundTransparency = 1.000
SectionTitle.BorderColor3 = Color3.fromRGB(0, 0, 0)
SectionTitle.BorderSizePixel = 0
SectionTitle.Position = UDim2.new(0.0500000007, 0, 0.0299999993, 0)
SectionTitle.Size = UDim2.new(0, 200, 0, 20)
SectionTitle.Font = Enum.Font.SourceSansBold
SectionTitle.Text = "Main Settings"
SectionTitle.TextColor3 = Color3.fromRGB(207, 207, 207)
SectionTitle.TextSize = 14.000
SectionTitle.TextXAlignment = Enum.TextXAlignment.Left

local SectionTitleStroke = Instance.new("UIStroke")
SectionTitleStroke.Parent = SectionTitle
SectionTitleStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual
SectionTitleStroke.Color = Color3.fromRGB(0, 0, 0)
SectionTitleStroke.Thickness = 1
SectionTitleStroke.Transparency = 0

local AimbotRow = Instance.new("Frame")
AimbotRow.Parent = MainContentPanel
AimbotRow.BackgroundTransparency = 1.000
AimbotRow.Position = UDim2.new(0.0700000003, 0, 0.100000001, 0)
AimbotRow.Size = UDim2.new(0, 150, 0, 20)
AimbotRow.ZIndex = 5

local AimbotToggle = Instance.new("TextButton")
AimbotToggle.Parent = AimbotRow
AimbotToggle.BackgroundColor3 = Color3.fromRGB(33, 33, 33)
AimbotToggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
AimbotToggle.BorderSizePixel = 0
AimbotToggle.Position = UDim2.new(0, 0, 1.04999995, 0)
AimbotToggle.Size = UDim2.new(0, 14, 0, 14)
AimbotToggle.ZIndex = 5
AimbotToggle.Font = Enum.Font.SourceSans
AimbotToggle.Text = ""
AimbotToggle.TextColor3 = Color3.fromRGB(0, 0, 0)
AimbotToggle.TextSize = 14.000

local AimbotToggleBorder = Instance.new("UIStroke")
AimbotToggleBorder.Parent = AimbotToggle
AimbotToggleBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
AimbotToggleBorder.Color = Color3.fromRGB(150, 190, 255)
AimbotToggleBorder.Thickness = 0.6
AimbotToggleBorder.Transparency = 0

local AimbotToggleFill = Instance.new("Frame")
AimbotToggleFill.Parent = AimbotToggle
AimbotToggleFill.BackgroundColor3 = Color3.fromRGB(150, 190, 255)
AimbotToggleFill.BorderSizePixel = 0
AimbotToggleFill.Position = UDim2.new(0, 2, 0, 2)
AimbotToggleFill.Size = UDim2.new(0, 0, 0, 0)
AimbotToggleFill.ZIndex = 6

local AimbotLabel = Instance.new("TextLabel")
AimbotLabel.Parent = AimbotRow
AimbotLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
AimbotLabel.BackgroundTransparency = 1.000
AimbotLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
AimbotLabel.BorderSizePixel = 0
AimbotLabel.Position = UDim2.new(0, 20, 0, 21)
AimbotLabel.Size = UDim2.new(0, 130, 0, 14)
AimbotLabel.ZIndex = 5
AimbotLabel.Font = Enum.Font.SourceSansBold
AimbotLabel.Text = "Aimbot"
AimbotLabel.TextColor3 = Color3.fromRGB(207, 207, 207)
AimbotLabel.TextSize = 12.000
AimbotLabel.TextXAlignment = Enum.TextXAlignment.Left

local AimbotLabelStroke = Instance.new("UIStroke")
AimbotLabelStroke.Parent = AimbotLabel
AimbotLabelStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual
AimbotLabelStroke.Color = Color3.fromRGB(0, 0, 0)
AimbotLabelStroke.Thickness = 1
AimbotLabelStroke.Transparency = 0

local SilentAimRow = Instance.new("Frame")
SilentAimRow.Parent = MainContentPanel
SilentAimRow.BackgroundTransparency = 1.000
SilentAimRow.Position = UDim2.new(0.0700000003, 0, 0.24000001, 0)
SilentAimRow.Size = UDim2.new(0, 150, 0, 20)
SilentAimRow.ZIndex = 5

local SilentAimToggle = Instance.new("TextButton")
SilentAimToggle.Parent = SilentAimRow
SilentAimToggle.BackgroundColor3 = Color3.fromRGB(33, 33, 33)
SilentAimToggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
SilentAimToggle.BorderSizePixel = 0
SilentAimToggle.Size = UDim2.new(0, 14, 0, 14)
SilentAimToggle.ZIndex = 5
SilentAimToggle.Font = Enum.Font.SourceSans
SilentAimToggle.Text = ""
SilentAimToggle.TextColor3 = Color3.fromRGB(0, 0, 0)
SilentAimToggle.TextSize = 14.000

local SilentAimToggleBorder = Instance.new("UIStroke")
SilentAimToggleBorder.Parent = SilentAimToggle
SilentAimToggleBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
SilentAimToggleBorder.Color = Color3.fromRGB(150, 190, 255)
SilentAimToggleBorder.Thickness = 0.6
SilentAimToggleBorder.Transparency = 0

local SilentAimToggleFill = Instance.new("Frame")
SilentAimToggleFill.Parent = SilentAimToggle
SilentAimToggleFill.BackgroundColor3 = Color3.fromRGB(150, 190, 255)
SilentAimToggleFill.BorderSizePixel = 0
SilentAimToggleFill.Position = UDim2.new(0, 2, 0, 2)
SilentAimToggleFill.Size = UDim2.new(0, 0, 0, 0)
SilentAimToggleFill.ZIndex = 6

local SilentAimLabel = Instance.new("TextLabel")
SilentAimLabel.Parent = SilentAimRow
SilentAimLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
SilentAimLabel.BackgroundTransparency = 1.000
SilentAimLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
SilentAimLabel.BorderSizePixel = 0
SilentAimLabel.Position = UDim2.new(0, 20, 0, 0)
SilentAimLabel.Size = UDim2.new(0, 130, 0, 14)
SilentAimLabel.ZIndex = 5
SilentAimLabel.Font = Enum.Font.SourceSansBold
SilentAimLabel.Text = "Silent Aim"
SilentAimLabel.TextColor3 = Color3.fromRGB(207, 207, 207)
SilentAimLabel.TextSize = 12.000
SilentAimLabel.TextXAlignment = Enum.TextXAlignment.Left

local SilentAimLabelStroke = Instance.new("UIStroke")
SilentAimLabelStroke.Parent = SilentAimLabel
SilentAimLabelStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual
SilentAimLabelStroke.Color = Color3.fromRGB(0, 0, 0)
SilentAimLabelStroke.Thickness = 1
SilentAimLabelStroke.Transparency = 0

local TeamAimbotRow = Instance.new("Frame")
TeamAimbotRow.Parent = MainContentPanel
TeamAimbotRow.BackgroundTransparency = 1.000
TeamAimbotRow.Position = UDim2.new(0.0700000003, 0, 0.310000002, 0)
TeamAimbotRow.Size = UDim2.new(0, 150, 0, 20)
TeamAimbotRow.ZIndex = 5

local TeamAimbotToggle = Instance.new("TextButton")
TeamAimbotToggle.Parent = TeamAimbotRow
TeamAimbotToggle.BackgroundColor3 = Color3.fromRGB(33, 33, 33)
TeamAimbotToggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
TeamAimbotToggle.BorderSizePixel = 0
TeamAimbotToggle.Size = UDim2.new(0, 14, 0, 14)
TeamAimbotToggle.ZIndex = 5
TeamAimbotToggle.Font = Enum.Font.SourceSans
TeamAimbotToggle.Text = ""
TeamAimbotToggle.TextColor3 = Color3.fromRGB(0, 0, 0)
TeamAimbotToggle.TextSize = 14.000

local TeamAimbotToggleBorder = Instance.new("UIStroke")
TeamAimbotToggleBorder.Parent = TeamAimbotToggle
TeamAimbotToggleBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
TeamAimbotToggleBorder.Color = Color3.fromRGB(150, 190, 255)
TeamAimbotToggleBorder.Thickness = 0.6
TeamAimbotToggleBorder.Transparency = 0

local TeamAimbotToggleFill = Instance.new("Frame")
TeamAimbotToggleFill.Parent = TeamAimbotToggle
TeamAimbotToggleFill.BackgroundColor3 = Color3.fromRGB(150, 190, 255)
TeamAimbotToggleFill.BorderSizePixel = 0
TeamAimbotToggleFill.Position = UDim2.new(0, 2, 0, 2)
TeamAimbotToggleFill.Size = UDim2.new(0, 0, 0, 0)
TeamAimbotToggleFill.ZIndex = 6

local TeamAimbotLabel = Instance.new("TextLabel")
TeamAimbotLabel.Parent = TeamAimbotRow
TeamAimbotLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TeamAimbotLabel.BackgroundTransparency = 1.000
TeamAimbotLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
TeamAimbotLabel.BorderSizePixel = 0
TeamAimbotLabel.Position = UDim2.new(0, 20, 0, 0)
TeamAimbotLabel.Size = UDim2.new(0, 130, 0, 14)
TeamAimbotLabel.ZIndex = 5
TeamAimbotLabel.Font = Enum.Font.SourceSansBold
TeamAimbotLabel.Text = "Team Aimbot"
TeamAimbotLabel.TextColor3 = Color3.fromRGB(207, 207, 207)
TeamAimbotLabel.TextSize = 12.000
TeamAimbotLabel.TextXAlignment = Enum.TextXAlignment.Left

local TeamAimbotLabelStroke = Instance.new("UIStroke")
TeamAimbotLabelStroke.Parent = TeamAimbotLabel
TeamAimbotLabelStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual
TeamAimbotLabelStroke.Color = Color3.fromRGB(0, 0, 0)
TeamAimbotLabelStroke.Thickness = 1
TeamAimbotLabelStroke.Transparency = 0

local TeamAimbotInput = Instance.new("TextBox")
TeamAimbotInput.Parent = MainContentPanel
TeamAimbotInput.BackgroundColor3 = Color3.fromRGB(33, 33, 33)
TeamAimbotInput.BorderColor3 = Color3.fromRGB(0, 0, 0)
TeamAimbotInput.BorderSizePixel = 0
TeamAimbotInput.Position = UDim2.new(0.0699999779, 0, 0.396303594, 0)
TeamAimbotInput.Size = UDim2.new(0, 93, 0, 16)
TeamAimbotInput.ZIndex = 5
TeamAimbotInput.Font = Enum.Font.SourceSans
TeamAimbotInput.PlaceholderText = "Enter team.."
TeamAimbotInput.Text = ""
TeamAimbotInput.TextColor3 = Color3.fromRGB(225, 225, 225)
TeamAimbotInput.TextSize = 10.000

local TeamAimbotInputBorder = Instance.new("UIStroke")
TeamAimbotInputBorder.Parent = TeamAimbotInput
TeamAimbotInputBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
TeamAimbotInputBorder.Color = Color3.fromRGB(150, 190, 255)
TeamAimbotInputBorder.Thickness = 0.6
TeamAimbotInputBorder.Transparency = 0

local UniversalESPRow = Instance.new("Frame")
UniversalESPRow.Parent = MainContentPanel
UniversalESPRow.BackgroundTransparency = 1.000
UniversalESPRow.Position = UDim2.new(0.400000006, 0, 0.100000001, 0)
UniversalESPRow.Size = UDim2.new(0, 150, 0, 20)
UniversalESPRow.ZIndex = 5

local UniversalESPToggle = Instance.new("TextButton")
UniversalESPToggle.Parent = UniversalESPRow
UniversalESPToggle.BackgroundColor3 = Color3.fromRGB(33, 33, 33)
UniversalESPToggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
UniversalESPToggle.BorderSizePixel = 0
UniversalESPToggle.Position = UDim2.new(0, 0, 4.19999981, 0)
UniversalESPToggle.Size = UDim2.new(0, 14, 0, 14)
UniversalESPToggle.ZIndex = 5
UniversalESPToggle.Font = Enum.Font.SourceSans
UniversalESPToggle.Text = ""
UniversalESPToggle.TextColor3 = Color3.fromRGB(0, 0, 0)
UniversalESPToggle.TextSize = 14.000

local UniversalESPToggleBorder = Instance.new("UIStroke")
UniversalESPToggleBorder.Parent = UniversalESPToggle
UniversalESPToggleBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
UniversalESPToggleBorder.Color = Color3.fromRGB(150, 190, 255)
UniversalESPToggleBorder.Thickness = 0.6
UniversalESPToggleBorder.Transparency = 0

local UniversalESPToggleFill = Instance.new("Frame")
UniversalESPToggleFill.Parent = UniversalESPToggle
UniversalESPToggleFill.BackgroundColor3 = Color3.fromRGB(150, 190, 255)
UniversalESPToggleFill.BorderSizePixel = 0
UniversalESPToggleFill.Position = UDim2.new(0, 2, 0, 2)
UniversalESPToggleFill.Size = UDim2.new(0, 0, 0, 0)
UniversalESPToggleFill.ZIndex = 6

local UniversalESPLabel = Instance.new("TextLabel")
UniversalESPLabel.Parent = UniversalESPRow
UniversalESPLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
UniversalESPLabel.BackgroundTransparency = 1.000
UniversalESPLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
UniversalESPLabel.BorderSizePixel = 0
UniversalESPLabel.Position = UDim2.new(0, 20, 0, 82)
UniversalESPLabel.Size = UDim2.new(0, 130, 0, 14)
UniversalESPLabel.ZIndex = 5
UniversalESPLabel.Font = Enum.Font.SourceSansBold
UniversalESPLabel.Text = "Universal ESP"
UniversalESPLabel.TextColor3 = Color3.fromRGB(207, 207, 207)
UniversalESPLabel.TextSize = 12.000
UniversalESPLabel.TextXAlignment = Enum.TextXAlignment.Left

local UniversalESPLabelStroke = Instance.new("UIStroke")
UniversalESPLabelStroke.Parent = UniversalESPLabel
UniversalESPLabelStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual
UniversalESPLabelStroke.Color = Color3.fromRGB(0, 0, 0)
UniversalESPLabelStroke.Thickness = 1
UniversalESPLabelStroke.Transparency = 0

local TracerRow = Instance.new("Frame")
TracerRow.Parent = MainContentPanel
TracerRow.BackgroundTransparency = 1.000
TracerRow.Position = UDim2.new(0.400000006, 0, 0.170000002, 0)
TracerRow.Size = UDim2.new(0, 150, 0, 20)
TracerRow.ZIndex = 5

local TracerToggle = Instance.new("TextButton")
TracerToggle.Parent = TracerRow
TracerToggle.BackgroundColor3 = Color3.fromRGB(33, 33, 33)
TracerToggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
TracerToggle.BorderSizePixel = 0
TracerToggle.Position = UDim2.new(0, 0, -0.0500000007, 0)
TracerToggle.Size = UDim2.new(0, 14, 0, 14)
TracerToggle.ZIndex = 5
TracerToggle.Font = Enum.Font.SourceSans
TracerToggle.Text = ""
TracerToggle.TextColor3 = Color3.fromRGB(0, 0, 0)
TracerToggle.TextSize = 14.000

local TracerToggleBorder = Instance.new("UIStroke")
TracerToggleBorder.Parent = TracerToggle
TracerToggleBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
TracerToggleBorder.Color = Color3.fromRGB(150, 190, 255)
TracerToggleBorder.Thickness = 0.6
TracerToggleBorder.Transparency = 0

local TracerToggleFill = Instance.new("Frame")
TracerToggleFill.Parent = TracerToggle
TracerToggleFill.BackgroundColor3 = Color3.fromRGB(150, 190, 255)
TracerToggleFill.BorderSizePixel = 0
TracerToggleFill.Position = UDim2.new(0, 2, 0, 2)
TracerToggleFill.Size = UDim2.new(0, 0, 0, 0)
TracerToggleFill.ZIndex = 6

local TracerLabel = Instance.new("TextLabel")
TracerLabel.Parent = TracerRow
TracerLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TracerLabel.BackgroundTransparency = 1.000
TracerLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
TracerLabel.BorderSizePixel = 0
TracerLabel.Position = UDim2.new(0, 20, 0, 0)
TracerLabel.Size = UDim2.new(0, 130, 0, 14)
TracerLabel.ZIndex = 5
TracerLabel.Font = Enum.Font.SourceSansBold
TracerLabel.Text = "Tracer"
TracerLabel.TextColor3 = Color3.fromRGB(207, 207, 207)
TracerLabel.TextSize = 12.000
TracerLabel.TextXAlignment = Enum.TextXAlignment.Left

local TracerLabelStroke = Instance.new("UIStroke")
TracerLabelStroke.Parent = TracerLabel
TracerLabelStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual
TracerLabelStroke.Color = Color3.fromRGB(0, 0, 0)
TracerLabelStroke.Thickness = 1
TracerLabelStroke.Transparency = 0

local PlayerESPRow = Instance.new("Frame")
PlayerESPRow.Parent = MainContentPanel
PlayerESPRow.BackgroundTransparency = 1.000
PlayerESPRow.Position = UDim2.new(0.400000006, 0, 0.24000001, 0)
PlayerESPRow.Size = UDim2.new(0, 150, 0, 20)
PlayerESPRow.ZIndex = 5

local PlayerESPToggle = Instance.new("TextButton")
PlayerESPToggle.Parent = PlayerESPRow
PlayerESPToggle.BackgroundColor3 = Color3.fromRGB(33, 33, 33)
PlayerESPToggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
PlayerESPToggle.BorderSizePixel = 0
PlayerESPToggle.Size = UDim2.new(0, 14, 0, 14)
PlayerESPToggle.ZIndex = 5
PlayerESPToggle.Font = Enum.Font.SourceSans
PlayerESPToggle.Text = ""
PlayerESPToggle.TextColor3 = Color3.fromRGB(0, 0, 0)
PlayerESPToggle.TextSize = 14.000

local PlayerESPToggleBorder = Instance.new("UIStroke")
PlayerESPToggleBorder.Parent = PlayerESPToggle
PlayerESPToggleBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
PlayerESPToggleBorder.Color = Color3.fromRGB(150, 190, 255)
Playe
