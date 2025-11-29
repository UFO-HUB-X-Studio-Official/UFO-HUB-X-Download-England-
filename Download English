--[[
    UFO HUB X • Download Screen (Letter-by-letter Title + BIG Flag)
    BG Image: 130548594326307
    Title: ขึ้นทีละตัวภายใน ~4 วินาที
    Rule สี: "UFO " สีขาว, "HUB X" สีเขียว
    Progress: 0 → 100% ภายใน 5 วินาที
    ธง 🇺🇸 ใหญ่กว่าหลอด download ชัดเจน แต่ยังเกาะปลายแท่งเขียว
    เสร็จแล้วทุกอย่างเฟดหายไป
]]

local Players      = game:GetService("Players")
local CoreGui      = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")

local lp = Players.LocalPlayer

-- ลบเก่าทิ้งก่อน
local OLD = CoreGui:FindFirstChild("UFOX_DownloadScreen")
if OLD then OLD:Destroy() end

local gui = Instance.new("ScreenGui")
gui.Name = "UFOX_DownloadScreen"
gui.IgnoreGuiInset = true
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Global
gui.Parent = CoreGui

-- พื้นหลัง
local bg = Instance.new("ImageLabel")
bg.Parent = gui
bg.Size = UDim2.fromScale(1,1)
bg.Position = UDim2.fromScale(0.5,0.5)
bg.AnchorPoint = Vector2.new(0.5,0.5)
bg.BackgroundTransparency = 1
bg.Image = "rbxassetid://130548594326307"
bg.ScaleType = Enum.ScaleType.Crop
bg.ImageTransparency = 0

-- TITLE "UFO HUB X" ขึ้นทีละตัว
-- กติกา: UFO = ขาว, HUB X = เขียว
local title = Instance.new("TextLabel")
title.Parent = gui
title.AnchorPoint = Vector2.new(0.5,0.5)
title.Position = UDim2.new(0.5,0,0.32,0)
title.Size = UDim2.new(0.8,0,0,90)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBlack
title.RichText = true
title.TextScaled = true
title.TextColor3 = Color3.new(1,1,1) -- base ขาว
title.TextStrokeColor3 = Color3.new(0,0,0)
title.TextStrokeTransparency = 0
title.Text = ""

local fullText = "UFO HUB X"
local totalTime = 4
local steps = #fullText
local stepDelay = totalTime / steps

task.spawn(function()
    for i = 1, #fullText do
        local text = fullText:sub(1, i)

        -- ตัวที่ 1–4 = "UFO " (ขาว)
        local whitePart = text:sub(1, math.min(4, #text))
        -- ตัวที่ 5 เป็นต้นไป = "HUB X" (เขียว)
        local greenPart = ""
        if #text > 4 then
            greenPart = text:sub(5)
        end

        local rich = whitePart
        if #greenPart > 0 then
            rich = string.format('%s<font color="rgb(25,255,125)">%s</font>', whitePart, greenPart)
        end

        title.Text = rich
        task.wait(stepDelay)
    end
end)

-- กล่องโหลด
local barHolder = Instance.new("Frame")
barHolder.Parent = gui
barHolder.AnchorPoint = Vector2.new(0.5,0.5)
barHolder.Position = UDim2.new(0.5,0,0.55,0)
barHolder.Size = UDim2.new(0.65,0,0,42)
barHolder.BackgroundColor3 = Color3.new(0,0,0)
barHolder.BackgroundTransparency = 0.25
barHolder.ClipsDescendants = false -- ให้ธงใหญ่กว่าแท่งได้

local corner = Instance.new("UICorner", barHolder)
corner.CornerRadius = UDim.new(0,16)

local stroke = Instance.new("UIStroke", barHolder)
stroke.Thickness = 2
stroke.Color = Color3.new(0,0,0)

-- Progress fill (สีเขียว)
local fill = Instance.new("Frame")
fill.Parent = barHolder
fill.AnchorPoint = Vector2.new(0,0.5)
fill.Position = UDim2.new(0,3,0.5,0)
fill.Size = UDim2.new(0,-6,1,-8)
fill.BackgroundColor3 = Color3.fromRGB(25,255,125)
fill.BackgroundTransparency = 0
fill.ClipsDescendants = false

local fillCorner = Instance.new("UICorner", fill)
fillCorner.CornerRadius = UDim.new(0,14)

-- ธง 🇺🇸 ใหญ่กว่าหลอด download ชัดเจน
local flag = Instance.new("TextLabel")
flag.Parent = fill
flag.BackgroundTransparency = 1
flag.AnchorPoint = Vector2.new(0.5,0.5)
flag.Position = UDim2.new(1, 24, 0.5, 0)   -- ยื่นออกไปทางขวานิดนึง
flag.Size = UDim2.new(0, 68, 0, 68)        -- สูง/กว้าง ใหญ่กว่าหลอด (42px)
flag.Font = Enum.Font.GothamBold
flag.TextScaled = true
flag.Text = "🇺🇸"
flag.ZIndex = 20

-- ข้อความ Download
local label = Instance.new("TextLabel")
label.Parent = barHolder
label.BackgroundTransparency = 1
label.Size = UDim2.new(1,0,1,0)
label.Font = Enum.Font.GothamBold
label.TextColor3 = Color3.new(1,1,1)
label.TextStrokeColor3 = Color3.new(0,0,0)
label.TextStrokeTransparency = 0
label.TextScaled = false
label.TextSize = 20
label.Text = "Download 0%"
label.ZIndex = 30

-- โหลด 0 → 100
local duration = 5
local delayStep = duration / 100

task.spawn(function()
    for i = 0,100 do
        local alpha = i / 100
        fill.Size = UDim2.new(alpha, -6, 1, -8)
        label.Text = ("Download %d%%"):format(i)
        task.wait(delayStep)
    end

    -- fade out
    local fade = 0.6

    TweenService:Create(bg, TweenInfo.new(fade), {ImageTransparency = 1}):Play()
    TweenService:Create(title, TweenInfo.new(fade), {TextTransparency = 1}):Play()
    TweenService:Create(label, TweenInfo.new(fade), {TextTransparency = 1}):Play()
    TweenService:Create(barHolder, TweenInfo.new(fade), {BackgroundTransparency = 1}):Play()
    TweenService:Create(fill, TweenInfo.new(fade), {BackgroundTransparency = 1}):Play()

    task.wait(fade + 0.2)
    gui:Destroy()
end)
