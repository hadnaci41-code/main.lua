-- Tsunde1eee GUI (Text Color: Black)
local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local LocalPlayer = Players.LocalPlayer

-- สร้าง ScreenGui (พยายามใส่ใน CoreGui ก่อน ถ้าไม่ได้จะลง PlayerGui)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "Tsunde1eeeGUI"
ScreenGui.ResetOnSpawn = false

local success = pcall(function()
    ScreenGui.Parent = CoreGui
end)
if not success then
    ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
end

-- 1. ปุ่มไอคอนเปิด-ปิด GUI (ลากย้ายได้)
local ToggleIcon = Instance.new("ImageButton")
ToggleIcon.Name = "ToggleIcon"
ToggleIcon.Size = UDim2.new(0, 50, 0, 50)
ToggleIcon.Position = UDim2.new(0.05, 0, 0.25, 0)
ToggleIcon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ToggleIcon.Image = "rbxassetid://132517293193890"
ToggleIcon.Active = true
ToggleIcon.Draggable = true
ToggleIcon.Parent = ScreenGui

local IconCorner = Instance.new("UICorner")
IconCorner.CornerRadius = UDim.new(0, 12)
IconCorner.Parent = ToggleIcon

local IconStroke = Instance.new("UIStroke")
IconStroke.Color = Color3.fromRGB(0, 255, 255) -- กรอบบางสี Cyan
IconStroke.Thickness = 1.5
IconStroke.Parent = ToggleIcon

-- 2. หน้าต่างหลัก GUI (พื้นหลังขาว กรอบบางสี Cyan)
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 240, 0, 150)
MainFrame.Position = UDim2.new(0.5, -120, 0.5, -75)
MainFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Visible = true
MainFrame.Parent = ScreenGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 10)
MainCorner.Parent = MainFrame

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = Color3.fromRGB(0, 255, 255) -- กรอบบางสี Cyan
MainStroke.Thickness = 1.5
MainStroke.Parent = MainFrame

-- 3. ช่องหัวข้อ "Tsunde1eee gui"
local HeaderFrame = Instance.new("Frame")
HeaderFrame.Name = "HeaderFrame"
HeaderFrame.Size = UDim2.new(1, 0, 0, 38)
HeaderFrame.BackgroundColor3 = Color3.fromRGB(245, 252, 255)
HeaderFrame.BorderSizePixel = 0
HeaderFrame.Parent = MainFrame

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 10)
HeaderCorner.Parent = HeaderFrame

-- เส้นแบ่งใต้หัวข้อสี Cyan บางๆ
local Divider = Instance.new("Frame")
Divider.Name = "Divider"
Divider.Size = UDim2.new(1, 0, 0, 1.5)
Divider.Position = UDim2.new(0, 0, 1, 0)
Divider.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
Divider.BorderSizePixel = 0
Divider.Parent = HeaderFrame

local TitleLabel = Instance.new("TextLabel")
TitleLabel.Name = "TitleLabel"
TitleLabel.Size = UDim2.new(1, 0, 1, 0)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "Tsunde1eee gui"
TitleLabel.TextColor3 = Color3.fromRGB(0, 0, 0) -- ตัวหนังสือสีดำสนิท
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextSize = 16
TitleLabel.Parent = HeaderFrame

-- 4. ช่องใส่ฟังก์ชันด้านล่าง
local ContentFrame = Instance.new("Frame")
ContentFrame.Name = "ContentFrame"
ContentFrame.Size = UDim2.new(1, 0, 1, -40)
ContentFrame.Position = UDim2.new(0, 0, 0, 40)
ContentFrame.BackgroundTransparency = 1
ContentFrame.Parent = MainFrame

-- ปุ่ม "Troll lag"
local TrollLagBtn = Instance.new("TextButton")
TrollLagBtn.Name = "TrollLagButton"
TrollLagBtn.Size = UDim2.new(0.85, 0, 0, 45)
TrollLagBtn.Position = UDim2.new(0.075, 0, 0.25, 0)
TrollLagBtn.BackgroundColor3 = Color3.fromRGB(245, 245, 245)
TrollLagBtn.Text = "Troll lag : OFF"
TrollLagBtn.TextColor3 = Color3.fromRGB(0, 0, 0) -- ตัวหนังสือสีดำสนิท
TrollLagBtn.Font = Enum.Font.GothamSemibold
TrollLagBtn.TextSize = 15
TrollLagBtn.Parent = ContentFrame

local BtnCorner = Instance.new("UICorner")
BtnCorner.CornerRadius = UDim.new(0, 8)
BtnCorner.Parent = TrollLagBtn

local BtnStroke = Instance.new("UIStroke")
BtnStroke.Color = Color3.fromRGB(0, 255, 255)
BtnStroke.Thickness = 1.2
BtnStroke.Parent = TrollLagBtn

-- ระบบทำงานของปุ่มเปิด-ปิด GUI
ToggleIcon.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

-- ระบบทำงานของฟังก์ชัน Troll lag (ล็อกตัวละครแต่หมุนจอได้)
local isTrollLag = false

local function setCharacterFreeze(state)
    local character = LocalPlayer.Character
    if character then
        local hrp = character:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp.Anchored = state
        end
    end
end

TrollLagBtn.MouseButton1Click:Connect(function()
    isTrollLag = not isTrollLag
    setCharacterFreeze(isTrollLag)
    
    if isTrollLag then
        TrollLagBtn.Text = "Troll lag : ON"
        TrollLagBtn.TextColor3 = Color3.fromRGB(0, 0, 0) -- ตัวหนังสือยังคงสีดำตอนเปิด
        TrollLagBtn.BackgroundColor3 = Color3.fromRGB(210, 255, 255)
    else
        TrollLagBtn.Text = "Troll lag : OFF"
        TrollLagBtn.TextColor3 = Color3.fromRGB(0, 0, 0) -- ตัวหนังสือสีดำตอนปิด
        TrollLagBtn.BackgroundColor3 = Color3.fromRGB(245, 245, 245)
    end
end)

-- กันบั๊กเวลาตัวละครตายแล้วเกิดใหม่ ให้รีเซ็ตสถานะปุ่มอัตโนมัติ
LocalPlayer.CharacterAdded:Connect(function()
    isTrollLag = false
    TrollLagBtn.Text = "Troll lag : OFF"
    TrollLagBtn.TextColor3 = Color3.fromRGB(0, 0, 0)
    TrollLagBtn.BackgroundColor3 = Color3.fromRGB(245, 245, 245)
end)
