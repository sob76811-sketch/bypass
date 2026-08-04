local a = game:GetService("Players")
local b = game:GetService("CoreGui")
local c = game:GetService("TweenService")
local d = game:GetService("UserInputService")
local e = a.LocalPlayer 
local f = workspace.CurrentCamera

-- Limpieza preventiva de instancias previas
if b:FindFirstChild("HermanosCPLoader_Premium") then 
    b.HermanosCPLoader_Premium:Destroy() 
end
if e:FindFirstChild("PlayerGui") and e.PlayerGui:FindFirstChild("HermanosCPLoader_Premium") then 
    e.PlayerGui.HermanosCPLoader_Premium:Destroy() 
end

local g = (e.LocaleId and e.LocaleId:lower()) or "es"
local h = not g:match("^es")

local function i() return (f and f.ViewportSize.X) or 800 end
local function j() return i() < 700 end
local function k(l) if l or j() then return math.clamp(math.floor(i()*0.88), 280, 360) end return 390 end

local n = {
    es = {
        choose = "Elige tu dispositivo:", 
        pc = "PC / COMPUTADORA", 
        pcD = "Menu completo en pantalla.", 
        mob = "CELULAR / MOVIL", 
        mobD = "Bolita flotante para abrir el menu.", 
        requesting = "[HCP] Cargando script ", 
        kickLoad = "Hermanos CP // Error al cargar script", 
        protected = "Protected | Unified Edition"
    },
    en = {
        choose = "Choose your device:", 
        pc = "PC / COMPUTER", 
        pcD = "Full on-screen menu.", 
        mob = "PHONE / MOBILE", 
        mobD = "Floating ball to open menu.", 
        requesting = "[HCP] Loading script ", 
        kickLoad = "Hermanos CP // Error loading script", 
        protected = "Protected | Unified Edition"
    }
}

local function o() return h and n.en or n.es end
local function p()
    local ok, res = pcall(function() return b end)
    if ok and res then return res end
    return e:WaitForChild("PlayerGui", 10) or b
end

-- SCRIPT PRINCIPAL OPTIMIZADO (COMPATIBLE CON XENO Y DELTA)
local function runUnifiedScript()
    local Players = game:GetService("Players")
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    local StarterPack = game:GetService("StarterPack")
    local RunService = game:GetService("RunService")
    local UserInputService = game:GetService("UserInputService")
    local Stats = game:GetService("Stats")
    local CoreGuiService = game:GetService("CoreGui")
    local TweenService = game:GetService("TweenService")
    local HttpService = game:GetService("HttpService")

    local _HCP_LANG = (type(_G) == "table" and _G.HCP_LANG) or nil
    if not _HCP_LANG then
        local lp = Players.LocalPlayer
        local loc = (lp and lp.LocaleId and lp.LocaleId:lower()) or "es"
        _HCP_LANG = loc:match("^es") and "es" or "en"
    end

    local _L = (_HCP_LANG == "en") and {
        title = "HERMANOS CP v6.2 // UNIFIED",
        tabMain = "MAIN",
        tabCfg = "CONFIG",
        aimbot = "AIMBOT",
        esp = "ESP VISUALS",
        inv = "INV VIEW",
        tracers = "TRACERS",
        cfgSys = "CONFIG SYSTEM",
        saveCfg = "SAVE",
        loadCfg = "LOAD",
        saved = "SAVED",
        loaded = "LOADED",
        aimMode = "AIM MODE",
        rpgMode = "RPG MODE",
        rpgToggle = "RPG MODE",
        fovSize = "FOV SIZE",
        smooth = "AIM STRENGTH",
        target = "AIM TARGET",
        skel = "SKELETON ESP",
        legAura = "LEGENDARY AURA",
        distEsp = "ESP DISTANCE: %s STUDS",
        binds = "KEYBINDS",
        pressKey = "...Press key!...",
        modeToggle = "Key",
        modeFov = "FOV",
        modeHold = "Hold",
        rpgDuro = "Hard",
        rpgBacio = "Soft",
        rpgNormal = "Normal",
        head = "Head",
        chest = "Chest",
        mixed = "Mixed",
        low = "Hard",
        mid = "Normal",
        high = "Soft",
        off = "Off",
        gold = "Gold",
        white = "White",
        ally = "ALLY",
        targetTag = "TARGET",
        aiming = "AIMING",
        team = "Team",
        noTeam = "No Team",
        pin = "Pin",
        unpin = "Unpin",
        on = "ON",
        offLabel = "OFF"
    } or {
        title = "HERMANOS CP v6.2 // UNIFIED",
        tabMain = "PRINCIPAL",
        tabCfg = "CONFIG",
        aimbot = "AIMBOT",
        esp = "ESP VISUALS",
        inv = "INV VIEW",
        tracers = "LÍNEAS",
        cfgSys = "SISTEMA DE CONFIG",
        saveCfg = "GUARDAR",
        loadCfg = "CARGAR",
        saved = "GUARDADO",
        loaded = "CARGADO",
        aimMode = "MODO DE AIM",
        rpgMode = "MODO RPG",
        rpgToggle = "MODO RPG",
        fovSize = "TAMAÑO FOV",
        smooth = "POTENCIA DE AIM",
        target = "OBJETIVO DE AIM",
        skel = "ESP PALITOS",
        legAura = "AURA LEGENDARIAS",
        distEsp = "DISTANCIA ESP: %s STUDS",
        binds = "TECLAS",
        pressKey = "...Presiona!...",
        modeToggle = "Tecla",
        modeFov = "FOV",
        modeHold = "Mando",
        rpgDuro = "Duro",
        rpgBacio = "Suave",
        rpgNormal = "Normal",
        head = "Cabeza",
        chest = "Pecho",
        mixed = "Mixto",
        low = "Duro",
        mid = "Normal",
        high = "Suave",
        off = "Off",
        gold = "Oro",
        white = "Blanco",
        ally = "ALIADO",
        targetTag = "TARGET",
        aiming = "APUNTANDO",
        team = "Team",
        noTeam = "No Team",
        pin = "Pin",
        unpin = "Unpin",
        on = "ON",
        offLabel = "OFF"
    }

    local function gEG(name)
        local genv = (type(getgenv) == "function" and getgenv()) or {}
        local fenv = (type(getfenv) == "function" and getfenv()) or {}
        local success, val = pcall(function()
            return genv[name] or fenv[name] or _G[name]
        end)
        return success and val or nil
    end

    local cloneref = gEG("cloneref")
    local Drawing = gEG("Drawing")
    local writefile = gEG("writefile")
    local readfile = gEG("readfile")
    local isfile = gEG("isfile")

    while not Players.LocalPlayer do task.wait(0.1) end
    local LocalPlayer = Players.LocalPlayer
    local Camera = workspace.CurrentCamera or workspace:WaitForChild("Camera")
    local CONFIG_FILE = "HermanosCP_Unified_Config.json"
    local sCfg, lCfg
    local targetController, smoothController, modeController, rpgController, skelController, legAuraController, rpgTogBtn

    local function getPingInSeconds()
        local ping = 0.04
        pcall(function()
            local rawPing = Stats.Network.ServerStatsItem["Data Ping"]:GetValue()
            ping = math.clamp(rawPing / 1000, 0.01, 0.5)
        end)
        return ping
    end

    local raycastParams = RaycastParams.new()
    raycastParams.FilterType = Enum.RaycastFilterType.Exclude
    raycastParams.IgnoreWater = true

    local tracerRayParams = RaycastParams.new()
    tracerRayParams.FilterType = Enum.RaycastFilterType.Exclude
    tracerRayParams.IgnoreWater = true

    local function getGroundPosition(originPos, targetChar)
        local filterList = {}
        if LocalPlayer.Character then table.insert(filterList, LocalPlayer.Character) end
        if targetChar then table.insert(filterList, targetChar) end
        raycastParams.FilterDescendantsInstances = filterList

        local rayResult = workspace:Raycast(originPos + Vector3.new(0, 4, 0), Vector3.new(0, -120, 0), raycastParams)
        if rayResult then return rayResult.Position end
        return originPos - Vector3.new(0, 3, 0)
    end

    local Track = { uid = nil, samples = {}, maxN = 14 }
    local function trackClear()
        Track.uid = nil
        table.clear(Track.samples)
    end
    local function trackSample(plr)
        if not plr or not plr.Character then return end
        local root = plr.Character:FindFirstChild("HumanoidRootPart")
        if not root then return end
        local uid = plr.UserId
        if Track.uid ~= uid then
            Track.uid = uid
            table.clear(Track.samples)
        end
        local now = tick()
        local vel = root.AssemblyLinearVelocity or root.Velocity or Vector3.zero
        table.insert(Track.samples, {
            t = now,
            pos = root.Position,
            hvel = Vector3.new(vel.X, 0, vel.Z),
        })
        while #Track.samples > Track.maxN do
            table.remove(Track.samples, 1)
        end
    end
    local function analyzeMotion()
        local s = Track.samples
        local n = #s
        if n < 2 then return Vector3.zero, Vector3.zero, 0, 0.25 end
        local sum = Vector3.zero
        for i = 1, n do sum = sum + s[i].hvel end
        local avgVel = sum / n
        local accel = Vector3.zero
        local accelCount = 0
        for i = 2, n do
            local dt = s[i].t - s[i - 1].t
            if dt > 0.001 and dt < 0.25 then
                accel = accel + ((s[i].hvel - s[i - 1].hvel) / dt)
                accelCount = accelCount + 1
            end
        end
        if accelCount > 0 then accel = accel / accelCount end
        if accel.Magnitude > 80 then accel = accel.Unit * 80 end
        local posVel = Vector3.zero
        local dtPos = s[n].t - s[1].t
        if dtPos > 0.05 then
            local dp = s[n].pos - s[1].pos
            posVel = Vector3.new(dp.X, 0, dp.Z) / dtPos
        end
        local blendVel = avgVel * 0.55 + posVel * 0.45
        return blendVel, accel, blendVel.Magnitude, math.clamp(n / Track.maxN, 0.3, 1)
    end

    local Config = {
        Theme = {
            Background      = Color3.fromRGB(11, 11, 18),
            Header          = Color3.fromRGB(16, 16, 26),
            Stroke          = Color3.fromRGB(0, 210, 255),
            StrokeInactive  = Color3.fromRGB(30, 30, 45),
            GradientStart   = Color3.fromRGB(18, 11, 32),
            GradientEnd     = Color3.fromRGB(7, 7, 12),
            PlayerRow       = Color3.fromRGB(20, 20, 30),
            PlayerRowPinned = Color3.fromRGB(38, 22, 58),
            TextPrimary     = Color3.fromRGB(255, 255, 255),
            TextSecondary   = Color3.fromRGB(160, 175, 210),
            PinActive       = Color3.fromRGB(0, 210, 255),
            PinInactive     = Color3.fromRGB(35, 35, 50),
            TeamActive      = Color3.fromRGB(0, 255, 140),
            EspNormal       = Color3.fromRGB(0, 210, 255),
            EspPinned       = Color3.fromRGB(255, 200, 0),
            EspTeam         = Color3.fromRGB(0, 255, 140),
            AuraFill        = Color3.fromRGB(255, 30, 30),
            BtnOn           = Color3.fromRGB(0, 255, 140),
            BtnOff          = Color3.fromRGB(255, 65, 95),
            CloseBtn        = Color3.fromRGB(35, 18, 26),
            CloseBtnText    = Color3.fromRGB(255, 80, 100),
            ScrollBar       = Color3.fromRGB(0, 210, 255),
            TabActive       = Color3.fromRGB(0, 210, 255),
            TabInactive     = Color3.fromRGB(22, 22, 35),
            Gold            = Color3.fromRGB(255, 215, 0),
            FOVNormal       = Color3.fromRGB(0, 210, 255),
            FOVLocked       = Color3.fromRGB(255, 65, 95)
        },
        Binds = {
            ToggleMenu = Enum.KeyCode.Z,
            Aimbot = Enum.KeyCode.F,
            InvView = Enum.KeyCode.X,
            GamepadAim = Enum.KeyCode.ButtonL2,
            GamepadToggle = Enum.KeyCode.DPadDown
        },
        AimTarget = "Mixto",
        RPGAimEnabled = false,
        RPGAimMode = "DURO",
        AimSmooth = "Bajo",
        AimMode   = "FOV",
        AimFOV    = 220,
        ShowFOV   = true,
        SkeletonStyle = "Oro",
        LegendaryAuraEnabled = true,
        MaxNormalDistance = 1200,
        MaxSpecialDistance = 1800,
        VehicleCameraFix = true,
        AimOrigin = "Cámara",
        AutoExecute = false,
        RPGRocketSpeed = 260
    }

    local State = {
        aimEnabled = true,
        espEnabled = true,
        invViewEnabled = true,
        tracersEnabled = true,
        holdingAimTrigger = false,
        isShooting = false,
        lockedTarget = nil,
        pinnedPlayers = {},
        autoPinned = {},
        teamPlayers = {},
        connections = {},
        alive = true,
        isBinding = nil,
        currentTab = "Principal"
    }

    local MasterObjects = {}
    local LastInventoryState = {}
    local ToolNameCache = {}
    local PlayerRowCache = {}
    local SkelCache = {}
    local LastToolScan = {}

    local function sC(signal, callback)
        local conn = signal:Connect(callback)
        table.insert(State.connections, conn)
        return conn
    end

    local nameCounter = 0
    local function gN()
        nameCounter = nameCounter + 1
        return string.char(math.random(65, 90)) .. string.char(math.random(97, 122)) .. tostring(math.random(100, 999)) .. tostring(nameCounter)
    end

    local HasDrawing = (type(Drawing) == "table" and type(Drawing.new) == "function")

    local function gSGP()
        local success, parent = pcall(function()
            local target = (type(cloneref) == "function" and cloneref(CoreGuiService)) or CoreGuiService
            local testGui = Instance.new("ScreenGui")
            testGui.Parent = target
            testGui:Destroy()
            return target
        end)
        if success and parent then return parent end
        return LocalPlayer:FindFirstChildOfClass("PlayerGui") or CoreGuiService
    end

    sC(workspace:GetPropertyChangedSignal("CurrentCamera"), function() Camera = workspace.CurrentCamera or Camera end)

    local function fCAO()
        if not Config.VehicleCameraFix then return end
        local char = LocalPlayer.Character
        if not char then return end
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum then
            if hum.CameraOffset ~= Vector3.zero then hum.CameraOffset = Vector3.zero end
            if Camera.CameraSubject ~= hum then Camera.CameraSubject = hum end
        end
        if Camera.CameraType ~= Enum.CameraType.Custom then Camera.CameraType = Enum.CameraType.Custom end
    end
    sC(Camera:GetPropertyChangedSignal("CameraSubject"), function() task.spawn(fCAO) end)
    sC(Camera:GetPropertyChangedSignal("CameraType"), function() task.spawn(fCAO) end)

    local humanoidConnection
    local function cH(hum)
        if humanoidConnection then humanoidConnection:Disconnect() end
        humanoidConnection = hum:GetPropertyChangedSignal("CameraOffset"):Connect(function()
            if Config.VehicleCameraFix and hum.CameraOffset ~= Vector3.zero then hum.CameraOffset = Vector3.zero end
        end)
        table.insert(State.connections, humanoidConnection)
    end

    sC(LocalPlayer.CharacterAdded, function(char)
        local hum = char:WaitForChild("Humanoid", 5)
        if hum then cH(hum) end
        task.spawn(fCAO)
    end)
    if LocalPlayer.Character then
        local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if hum then cH(hum) end
    end

    local function cAAT(player)
        if player == LocalPlayer then return end
        task.spawn(function()
            local success, isFriend = pcall(function() return LocalPlayer:IsFriendsWith(player.UserId) end)
            if success and isFriend then
                State.teamPlayers[player.Name] = true
                if State.lockedTarget == player then State.lockedTarget = nil end
            end
        end)
    end

    local function getMuzzlePosition()
        local char = LocalPlayer.Character
        if not char then return Camera.CFrame.Position end
        local tool = char:FindFirstChildOfClass("Tool")
        if tool then
            local handle = tool:FindFirstChild("Handle") or tool:FindFirstChild("Muzzle") or tool:FindFirstChild("Part")
            if handle then return handle.Position end
        end
        local arm = char:FindFirstChild("RightHand") or char:FindFirstChild("Right Arm")
        if arm then return arm.Position end
        return char:FindFirstChild("Head") and char.Head.Position or Camera.CFrame.Position
    end

    local function drawBulletTracer(fromPos, toPos)
        if not State.tracersEnabled then return end
        task.spawn(function()
            local distance = (toPos - fromPos).Magnitude
            if distance < 1 then return end

            local tracer = Instance.new("Part")
            tracer.Name = "HCP_Tracer"
            tracer.Anchored = true
            tracer.CanCollide = false
            tracer.Material = Enum.Material.Neon
            tracer.Color = Color3.fromRGB(0, 230, 255)
            tracer.Size = Vector3.new(0.08, 0.08, distance)
            tracer.CFrame = CFrame.new(fromPos, toPos) * CFrame.new(0, 0, -distance / 2)
            tracer.Parent = workspace

            local tween = TweenService:Create(tracer, TweenInfo.new(0.35, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
                Transparency = 1,
                Size = Vector3.new(0.01, 0.01, distance)
            })
            tween:Play()
            tween.Completed:Wait()
            tracer:Destroy()
        end)
    end

    local function cL()
        if not HasDrawing then return nil end
        local ok, l = pcall(Drawing.new, "Line")
        if ok and l then l.Thickness = 1.5; l.Transparency = 1; l.Visible = false; return l end
        return nil
    end

    local function gSk(plr)
        local name = plr.Name
        if not SkelCache[name] then
            SkelCache[name] = {
                Head_Spine = cL(), Spine_LeftArm = cL(), Spine_RightArm = cL(),
                LeftArm_Hand = cL(), RightArm_Hand = cL(), Spine_LeftLeg = cL(),
                Spine_RightLeg = cL(), LeftLeg_Foot = cL(), RightLeg_Foot = cL()
            }
        end
        return SkelCache[name]
    end

    local function hSk(plr)
        local sk = SkelCache[plr.Name]
        if sk then for _, l in pairs(sk) do if l then pcall(function() l.Visible = false end) end end end
    end

    local function hideAllSkeletons()
        for _, sk in pairs(SkelCache) do
            for _, l in pairs(sk) do if l then pcall(function() l.Visible = false end) end end
        end
    end

    local function uSE(plr, char)
        if not State.espEnabled or Config.SkeletonStyle == "Off" or not HasDrawing then hSk(plr); return end
        local sk = gSk(plr)
        local col = (Config.SkeletonStyle == "Oro") and Config.Theme.Gold or Color3.fromRGB(255, 255, 255)
        local function connJ(line, p1, p2)
            if not line then return end
            if p1 and p2 then
                local v1, vis1 = Camera:WorldToViewportPoint(p1.Position)
                local v2, vis2 = Camera:WorldToViewportPoint(p2.Position)
                if vis1 or vis2 then
                    pcall(function() line.From = Vector2.new(v1.X, v1.Y); line.To = Vector2.new(v2.X, v2.Y); line.Color = col; line.Visible = true end)
                    return
                end
            end
            pcall(function() line.Visible = false end)
        end
        if char:FindFirstChild("UpperTorso") then
            connJ(sk.Head_Spine, char:FindFirstChild("Head"), char:FindFirstChild("UpperTorso"))
            connJ(sk.Spine_LeftArm, char:FindFirstChild("UpperTorso"), char:FindFirstChild("LeftUpperArm"))
            connJ(sk.Spine_RightArm, char:FindFirstChild("UpperTorso"), char:FindFirstChild("RightUpperArm"))
            connJ(sk.LeftArm_Hand, char:FindFirstChild("LeftUpperArm"), char:FindFirstChild("LeftHand"))
            connJ(sk.RightArm_Hand, char:FindFirstChild("RightUpperArm"), char:FindFirstChild("RightHand"))
            connJ(sk.Spine_LeftLeg, char:FindFirstChild("LowerTorso"), char:FindFirstChild("LeftUpperLeg"))
            connJ(sk.Spine_RightLeg, char:FindFirstChild("LowerTorso"), char:FindFirstChild("RightUpperLeg"))
            connJ(sk.LeftLeg_Foot, char:FindFirstChild("LeftUpperLeg"), char:FindFirstChild("LeftFoot"))
            connJ(sk.RightLeg_Foot, char:FindFirstChild("RightUpperLeg"), char:FindFirstChild("RightFoot"))
        elseif char:FindFirstChild("Torso") then
            connJ(sk.Head_Spine, char:FindFirstChild("Head"), char:FindFirstChild("Torso"))
            connJ(sk.Spine_LeftArm, char:FindFirstChild("Torso"), char:FindFirstChild("Left Arm"))
            connJ(sk.Spine_RightArm, char:FindFirstChild("Torso"), char:FindFirstChild("Right Arm"))
            connJ(sk.Spine_LeftLeg, char:FindFirstChild("Torso"), char:FindFirstChild("Left Leg"))
            connJ(sk.Spine_RightLeg, char:FindFirstChild("Torso"), char:FindFirstChild("Right Leg"))
        else
            hSk(plr)
        end
    end

    local gui = Instance.new("ScreenGui")
    gui.Name = gN()
    gui.IgnoreGuiInset = true
    gui.ResetOnSpawn = false
    gui.Parent = gSGP()

    local cam = workspace.CurrentCamera
    local vw = (cam and cam.ViewportSize.X) or 800
    local vh = (cam and cam.ViewportSize.Y) or 600
    local isMobileUI = UserInputService.TouchEnabled and (not UserInputService.KeyboardEnabled or vw < 700)
    local frameW = isMobileUI and math.clamp(math.floor(vw * 0.92), 280, 380) or 460
    local frameH = isMobileUI and math.clamp(math.floor(vh * 0.72), 380, 480) or 520

    local MainFrame = Instance.new("Frame")
    MainFrame.Size = UDim2.new(0, frameW, 0, frameH)
    MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
    MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
    MainFrame.BackgroundColor3 = Config.Theme.Background
    MainFrame.ClipsDescendants = true
    MainFrame.Parent = gui

    Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 12)
    local mainStroke = Instance.new("UIStroke") mainStroke.Color = Config.Theme.Stroke; mainStroke.Thickness = 1.2; mainStroke.Parent = MainFrame

    local gradient = Instance.new("UIGradient")
    gradient.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Config.Theme.GradientStart),
        ColorSequenceKeypoint.new(1, Config.Theme.GradientEnd),
    })
    gradient.Parent = MainFrame

    local header = Instance.new("Frame")
    header.Size = UDim2.new(1, 0, 0, 45); header.BackgroundColor3 = Config.Theme.Header; header.Parent = MainFrame
    Instance.new("UICorner", header).CornerRadius = UDim.new(0, 12)

    local title = Instance.new("TextLabel")
    title.Font = Enum.Font.GothamBold; title.TextSize = 13; title.TextColor3 = Config.Theme.TextPrimary
    title.Size = UDim2.new(1, -80, 1, 0); title.Position = UDim2.new(0, 15, 0, 0); title.BackgroundTransparency = 1
    title.Text = _L.title; title.TextXAlignment = Enum.TextXAlignment.Left; title.Parent = header

    local minBtn = Instance.new("TextButton")
    minBtn.Size = UDim2.new(0, 28, 0, 28); minBtn.Position = UDim2.new(1, -70, 0.5, -14)
    minBtn.Text = "-"; minBtn.TextSize = 18; minBtn.Font = Enum.Font.GothamBold
    minBtn.TextColor3 = Color3.fromRGB(255, 210, 80); minBtn.BackgroundColor3 = Color3.fromRGB(40, 35, 18); minBtn.Parent = header
    Instance.new("UICorner", minBtn).CornerRadius = UDim.new(0, 6)

    local closeBtn = Instance.new("TextButton")
    closeBtn.Size = UDim2.new(0, 28, 0, 28); closeBtn.Position = UDim2.new(1, -38, 0.5, -14)
    closeBtn.Text = "X"; closeBtn.TextSize = 18; closeBtn.Font = Enum.Font.GothamBold
    closeBtn.TextColor3 = Config.Theme.CloseBtnText; closeBtn.BackgroundColor3 = Config.Theme.CloseBtn; closeBtn.Parent = header
    Instance.new("UICorner", closeBtn).CornerRadius = UDim.new(0, 6)

    closeBtn.MouseEnter:Connect(function() TweenService:Create(closeBtn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(80, 25, 40)}):Play() end)
    closeBtn.MouseLeave:Connect(function() TweenService:Create(closeBtn, TweenInfo.new(0.15), {BackgroundColor3 = Config.Theme.CloseBtn}):Play() end)

    local openBall = Instance.new("ImageButton")
    openBall.Name = "HCPOpenBall"; openBall.Size = UDim2.new(0, 50, 0, 50); openBall.Position = UDim2.new(1, -64, 0.55, 0)
    openBall.BackgroundColor3 = Color3.fromRGB(0, 160, 255); openBall.BorderSizePixel = 0; openBall.Visible = false; openBall.AutoButtonColor = false; openBall.Parent = gui
    Instance.new("UICorner", openBall).CornerRadius = UDim.new(1, 0)
    local openBallStroke = Instance.new("UIStroke") openBallStroke.Color = Color3.fromRGB(255, 255, 255); openBallStroke.Thickness = 2; openBallStroke.Transparency = 0.35; openBallStroke.Parent = openBall
    local openBallTxt = Instance.new("TextLabel") openBallTxt.Size = UDim2.new(1, 0, 1, 0); openBallTxt.BackgroundTransparency = 1; openBallTxt.Font = Enum.Font.GothamBold; openBallTxt.TextSize = 12; openBallTxt.TextColor3 = Color3.fromRGB(255, 255, 255); openBallTxt.Text = "HCP"; openBallTxt.Parent = openBall

    local ballDrag, ballStart, ballPos
    openBall.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then ballDrag = true; ballStart = input.Position; ballPos = openBall.Position end
    end)
    sC(UserInputService.InputChanged, function(input)
        if ballDrag and (input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseMovement) then
            local d = input.Position - ballStart
            openBall.Position = UDim2.new(ballPos.X.Scale, ballPos.X.Offset + d.X, ballPos.Y.Scale, ballPos.Y.Offset + d.Y)
        end
    end)
    sC(UserInputService.InputEnded, function(input)
        if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then ballDrag = false end
    end)
    openBall.MouseButton1Click:Connect(function() MainFrame.Visible = true; openBall.Visible = false end)
    minBtn.MouseButton1Click:Connect(function() MainFrame.Visible = false; openBall.Visible = true end)

    local TabBar = Instance.new("Frame") TabBar.Size = UDim2.new(1, -20, 0, 34); TabBar.Position = UDim2.new(0, 10, 0, 55); TabBar.BackgroundTransparency = 1; TabBar.Parent = MainFrame
    local tabLayout = Instance.new("UIListLayout") tabLayout.FillDirection = Enum.FillDirection.Horizontal; tabLayout.Padding = UDim.new(0, 8); tabLayout.Parent = TabBar

    local function cTB(text, parent)
        local btn = Instance.new("TextButton") btn.Size = UDim2.new(0.5, -4, 1, 0); btn.Font = Enum.Font.GothamBold; btn.TextSize = 11; btn.Text = text; btn.TextColor3 = Config.Theme.TextPrimary; btn.BackgroundColor3 = Config.Theme.TabInactive
        Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)
        local stroke = Instance.new("UIStroke") stroke.Thickness = 1; stroke.Color = Config.Theme.StrokeInactive; stroke.Parent = btn
        btn.Parent = parent
        return btn, stroke
    end

    local TabPrincipalBtn, tabPStroke = cTB(_L.tabMain, TabBar)
    local TabConfigBtn, tabCStroke = cTB(_L.tabCfg, TabBar)

    local ContentPrincipal = Instance.new("Frame") ContentPrincipal.Size = UDim2.new(1, -20, 1, -105); ContentPrincipal.Position = UDim2.new(0, 10, 0, 100); ContentPrincipal.BackgroundTransparency = 1; ContentPrincipal.Parent = MainFrame
    local ContentConfig = Instance.new("ScrollingFrame") ContentConfig.Size = UDim2.new(1, -20, 1, -105); ContentConfig.Position = UDim2.new(0, 10, 0, 100); ContentConfig.BackgroundTransparency = 1; ContentConfig.Visible = false; ContentConfig.AutomaticCanvasSize = Enum.AutomaticSize.Y; ContentConfig.ScrollBarThickness = 2; ContentConfig.ScrollBarImageColor3 = Config.Theme.ScrollBar; ContentConfig.Parent = MainFrame

    local function sT(tabName)
        State.currentTab = tabName
        local tInfo = TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
        if tabName == "Principal" then
            TweenService:Create(TabPrincipalBtn, tInfo, {BackgroundColor3 = Config.Theme.TabActive}):Play()
            TweenService:Create(TabConfigBtn, tInfo, {BackgroundColor3 = Config.Theme.TabInactive}):Play()
            TweenService:Create(tabPStroke, tInfo, {Color = Config.Theme.TabActive}):Play()
            TweenService:Create(tabCStroke, tInfo, {Color = Config.Theme.StrokeInactive}):Play()
            TabPrincipalBtn.TextColor3 = Color3.fromRGB(10, 10, 18); TabConfigBtn.TextColor3 = Config.Theme.TextPrimary
            ContentPrincipal.Visible = true; ContentConfig.Visible = false
        else
            TweenService:Create(TabPrincipalBtn, tInfo, {BackgroundColor3 = Config.Theme.TabInactive}):Play()
            TweenService:Create(TabConfigBtn, tInfo, {BackgroundColor3 = Config.Theme.TabActive}):Play()
            TweenService:Create(tabPStroke, tInfo, {Color = Config.Theme.StrokeInactive}):Play()
            TweenService:Create(tabCStroke, tInfo, {Color = Config.Theme.TabActive}):Play()
            TabPrincipalBtn.TextColor3 = Config.Theme.TextPrimary; TabConfigBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
            ContentPrincipal.Visible = false; ContentConfig.Visible = true
        end
    end
    sT("Principal")

    TabPrincipalBtn.MouseButton1Click:Connect(function() sT("Principal") end)
    TabConfigBtn.MouseButton1Click:Connect(function() sT("Config") end)

    local TogglePanel = Instance.new("Frame") TogglePanel.Size = UDim2.new(1, 0, 0, 35); TogglePanel.BackgroundTransparency = 1; TogglePanel.Parent = ContentPrincipal
    local grid = Instance.new("UIGridLayout") grid.CellSize = UDim2.new(0.235, 0, 0, 32); grid.CellPadding = UDim2.new(0, 5, 0, 5); grid.Parent = TogglePanel

    local function cTog(parent, text)
        local btn = Instance.new("TextButton") btn.Font = Enum.Font.GothamBold; btn.TextSize = 10; btn.TextColor3 = Config.Theme.TextPrimary; btn.Text = text
        Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)
        local btnStroke = Instance.new("UIStroke") btnStroke.Thickness = 1; btnStroke.Color = Color3.fromRGB(255,255,255); btnStroke.Transparency = 0.85; btnStroke.Parent = btn
        btn.Parent = parent
        return btn
    end

    local AimToggleBtn = cTog(TogglePanel, _L.aimbot)
    local EspToggleBtn = cTog(TogglePanel, _L.esp)
    local InvToggleBtn = cTog(TogglePanel, _L.inv)
    local TracerToggleBtn = cTog(TogglePanel, _L.tracers)

    local scroll = Instance.new("ScrollingFrame") scroll.Size = UDim2.new(1, 0, 1, -45); scroll.Position = UDim2.new(0, 0, 0, 45); scroll.BackgroundTransparency = 1; scroll.AutomaticCanvasSize = Enum.AutomaticSize.Y; scroll.ScrollBarThickness = 3; scroll.ScrollBarImageColor3 = Config.Theme.ScrollBar; scroll.Parent = ContentPrincipal
    local layout = Instance.new("UIListLayout") layout.SortOrder = Enum.SortOrder.LayoutOrder; layout.Padding = UDim.new(0, 6); layout.Parent = scroll

    local function uMB()
        local tInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
        TweenService:Create(AimToggleBtn, tInfo, {BackgroundColor3 = State.aimEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff}):Play()
        AimToggleBtn.Text = "AIM: " .. (State.aimEnabled and _L.on or _L.offLabel); AimToggleBtn.TextColor3 = State.aimEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
        
        TweenService:Create(EspToggleBtn, tInfo, {BackgroundColor3 = State.espEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff}):Play()
        EspToggleBtn.Text = "ESP: " .. (State.espEnabled and _L.on or _L.offLabel); EspToggleBtn.TextColor3 = State.espEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
        
        TweenService:Create(InvToggleBtn, tInfo, {BackgroundColor3 = State.invViewEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff}):Play()
        InvToggleBtn.Text = "INV: " .. (State.invViewEnabled and _L.on or _L.offLabel); InvToggleBtn.TextColor3 = State.invViewEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary

        TweenService:Create(TracerToggleBtn, tInfo, {BackgroundColor3 = State.tracersEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff}):Play()
        TracerToggleBtn.Text = _L.tracers .. ": " .. (State.tracersEnabled and _L.on or _L.offLabel); TracerToggleBtn.TextColor3 = State.tracersEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
    end
    uMB()

    AimToggleBtn.MouseButton1Click:Connect(function() State.aimEnabled = not State.aimEnabled; if not State.aimEnabled then State.lockedTarget = nil end; uMB(); sCfg() end)
    EspToggleBtn.MouseButton1Click:Connect(function() State.espEnabled = not State.espEnabled; if not State.espEnabled then hideAllSkeletons() end; uMB(); sCfg() end)
    InvToggleBtn.MouseButton1Click:Connect(function() State.invViewEnabled = not State.invViewEnabled; uMB(); sCfg() end)
    TracerToggleBtn.MouseButton1Click:Connect(function() State.tracersEnabled = not State.tracersEnabled; uMB(); sCfg() end)

    local function cCCS(titleText, buttonsData, callback)
        local sectionFrame = Instance.new("Frame") sectionFrame.Size = UDim2.new(1, 0, 0, 58); sectionFrame.BackgroundTransparency = 1
        local lbl = Instance.new("TextLabel") lbl.Size = UDim2.new(1, 0, 0, 18); lbl.Font = Enum.Font.GothamBold; lbl.TextSize = 11; lbl.TextColor3 = Config.Theme.TextSecondary; lbl.Text = titleText:upper(); lbl.TextXAlignment = Enum.TextXAlignment.Left; lbl.BackgroundTransparency = 1; lbl.Parent = sectionFrame
        
        local cycleBtn = Instance.new("TextButton") cycleBtn.Size = UDim2.new(1, 0, 0, 32); cycleBtn.Position = UDim2.new(0, 0, 0, 22); cycleBtn.Font = Enum.Font.GothamBold; cycleBtn.TextSize = 10; cycleBtn.BackgroundColor3 = Config.Theme.TabInactive; cycleBtn.TextColor3 = Config.Theme.TextPrimary
        Instance.new("UICorner", cycleBtn).CornerRadius = UDim.new(0, 6)
        local optStroke = Instance.new("UIStroke") optStroke.Thickness = 1; optStroke.Color = Config.Theme.StrokeInactive; optStroke.Parent = cycleBtn
        
        local currentIndex = 1
        local function updateText() cycleBtn.Text = ">  " .. buttonsData[currentIndex].Label:upper() .. "  <" end
        
        cycleBtn.MouseButton1Click:Connect(function()
            currentIndex = (currentIndex % #buttonsData) + 1
            local chosenOpt = buttonsData[currentIndex]
            callback(chosenOpt.Value)
            updateText()
            TweenService:Create(cycleBtn, TweenInfo.new(0.1), {BackgroundColor3 = Config.Theme.TabActive}):Play()
            cycleBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
            task.delay(0.15, function()
                TweenService:Create(cycleBtn, TweenInfo.new(0.15), {BackgroundColor3 = Config.Theme.TabInactive}):Play()
                cycleBtn.TextColor3 = Config.Theme.TextPrimary
            end)
            sCfg()
        end)
        cycleBtn.Parent = sectionFrame; sectionFrame.Parent = ContentConfig
        
        local controller = {}
        function controller.setValue(val)
            for i, opt in ipairs(buttonsData) do
                if opt.Value == val then currentIndex = i; updateText(); break end
            end
        end
        return controller
    end

    Instance.new("UIListLayout", ContentConfig).SortOrder = Enum.SortOrder.LayoutOrder
    ContentConfig.UIListLayout.Padding = UDim.new(0, 14)

    local saveLoadSection = Instance.new("Frame") saveLoadSection.Size = UDim2.new(1, 0, 0, 58); saveLoadSection.BackgroundTransparency = 1; saveLoadSection.Parent = ContentConfig
    local saveLoadLbl = Instance.new("TextLabel") saveLoadLbl.Size = UDim2.new(1, 0, 0, 18); saveLoadLbl.Font = Enum.Font.GothamBold; saveLoadLbl.TextSize = 11; saveLoadLbl.TextColor3 = Config.Theme.TextSecondary; saveLoadLbl.Text = _L.cfgSys; saveLoadLbl.TextXAlignment = Enum.TextXAlignment.Left; saveLoadLbl.BackgroundTransparency = 1; saveLoadLbl.Parent = saveLoadSection

    local slContainer = Instance.new("Frame") slContainer.Size = UDim2.new(1, 0, 0, 32); slContainer.Position = UDim2.new(0, 0, 0, 22); slContainer.BackgroundTransparency = 1; slContainer.Parent = saveLoadSection
    local slLayout = Instance.new("UIListLayout") slLayout.FillDirection = Enum.FillDirection.Horizontal; slLayout.Padding = UDim.new(0, 8); slLayout.Parent = slContainer

    local saveBtn = Instance.new("TextButton") saveBtn.Size = UDim2.new(0.5, -4, 1, 0); saveBtn.Font = Enum.Font.GothamBold; saveBtn.TextSize = 10; saveBtn.BackgroundColor3 = Config.Theme.TabInactive; saveBtn.TextColor3 = Config.Theme.TextPrimary; saveBtn.Text = _L.saveCfg; saveBtn.Parent = slContainer
    Instance.new("UICorner", saveBtn).CornerRadius = UDim.new(0, 6)

    local loadBtn = Instance.new("TextButton") loadBtn.Size = UDim2.new(0.5, -4, 1, 0); loadBtn.Font = Enum.Font.GothamBold; loadBtn.TextSize = 10; loadBtn.BackgroundColor3 = Config.Theme.TabInactive; loadBtn.TextColor3 = Config.Theme.TextPrimary; loadBtn.Text = _L.loadCfg; loadBtn.Parent = slContainer
    Instance.new("UICorner", loadBtn).CornerRadius = UDim.new(0, 6)

    local rpgTogFrame = Instance.new("Frame") rpgTogFrame.Size = UDim2.new(1, 0, 0, 32); rpgTogFrame.BackgroundTransparency = 1; rpgTogFrame.Parent = ContentConfig
    rpgTogBtn = Instance.new("TextButton") rpgTogBtn.Size = UDim2.new(0.72, -4, 1, 0); rpgTogBtn.Font = Enum.Font.GothamBold; rpgTogBtn.TextSize = 10; rpgTogBtn.BackgroundColor3 = Config.RPGAimEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff; rpgTogBtn.TextColor3 = Config.RPGAimEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary; rpgTogBtn.Text = _L.rpgToggle .. ": " .. (Config.RPGAimEnabled and _L.on or _L.offLabel); rpgTogBtn.Parent = rpgTogFrame
    Instance.new("UICorner", rpgTogBtn).CornerRadius = UDim.new(0, 6)

    local betaBadge = Instance.new("TextLabel") betaBadge.Size = UDim2.new(0.28, -2, 1, 0); betaBadge.Position = UDim2.new(0.72, 4, 0, 0); betaBadge.BackgroundColor3 = Color3.fromRGB(255, 60, 60); betaBadge.Font = Enum.Font.GothamBold; betaBadge.TextSize = 10; betaBadge.TextColor3 = Color3.fromRGB(255, 255, 255); betaBadge.Text = "BETA"; betaBadge.Parent = rpgTogFrame
    Instance.new("UICorner", betaBadge).CornerRadius = UDim.new(0, 6)

    local function uRPG()
        local tInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
        TweenService:Create(rpgTogBtn, tInfo, {BackgroundColor3 = Config.RPGAimEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff}):Play()
        rpgTogBtn.Text = _L.rpgToggle .. ": " .. (Config.RPGAimEnabled and _L.on or _L.offLabel)
        rpgTogBtn.TextColor3 = Config.RPGAimEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
    end

    rpgTogBtn.MouseButton1Click:Connect(function() Config.RPGAimEnabled = not Config.RPGAimEnabled; uRPG(); sCfg() end)

    local fovSection = Instance.new("Frame") fovSection.Size = UDim2.new(1, 0, 0, 70); fovSection.BackgroundTransparency = 1; fovSection.Parent = ContentConfig
    local fovLbl = Instance.new("TextLabel") fovLbl.Size = UDim2.new(1, -60, 0, 18); fovLbl.Font = Enum.Font.GothamBold; fovLbl.TextSize = 11; fovLbl.TextColor3 = Config.Theme.TextSecondary; fovLbl.Text = _L.fovSize; fovLbl.TextXAlignment = Enum.TextXAlignment.Left; fovLbl.BackgroundTransparency = 1; fovLbl.Parent = fovSection
    local fovValueLbl = Instance.new("TextLabel") fovValueLbl.Size = UDim2.new(0, 55, 0, 18); fovValueLbl.Position = UDim2.new(1, -55, 0, 0); fovValueLbl.Font = Enum.Font.GothamBold; fovValueLbl.TextSize = 12; fovValueLbl.TextColor3 = Config.Theme.TabActive; fovValueLbl.Text = tostring(Config.AimFOV); fovValueLbl.TextXAlignment = Enum.TextXAlignment.Right; fovValueLbl.BackgroundTransparency = 1; fovValueLbl.Parent = fovSection

    local FOV_MIN, FOV_MAX = 40, 400
    local fovTrack = Instance.new("Frame") fovTrack.Size = UDim2.new(1, 0, 0, 16); fovTrack.Position = UDim2.new(0, 0, 0, 32); fovTrack.BackgroundColor3 = Config.Theme.TabInactive; fovTrack.BorderSizePixel = 0; fovTrack.Parent = fovSection
    Instance.new("UICorner", fovTrack).CornerRadius = UDim.new(1, 0)

    local fovFill = Instance.new("Frame") fovFill.Size = UDim2.new(math.clamp((Config.AimFOV - FOV_MIN) / (FOV_MAX - FOV_MIN), 0, 1), 0, 1, 0); fovFill.BackgroundColor3 = Config.Theme.TabActive; fovFill.BorderSizePixel = 0; fovFill.Parent = fovTrack
    Instance.new("UICorner", fovFill).CornerRadius = UDim.new(1, 0)

    local fovKnob = Instance.new("Frame") fovKnob.Size = UDim2.new(0, 22, 0, 22); fovKnob.AnchorPoint = Vector2.new(0.5, 0.5); fovKnob.Position = UDim2.new(math.clamp((Config.AimFOV - FOV_MIN) / (FOV_MAX - FOV_MIN), 0, 1), 0, 0.5, 0); fovKnob.BackgroundColor3 = Color3.fromRGB(255, 255, 255); fovKnob.BorderSizePixel = 0; fovKnob.ZIndex = 2; fovKnob.Parent = fovTrack
    Instance.new("UICorner", fovKnob).CornerRadius = UDim.new(1, 0)
    local fovKnobStroke = Instance.new("UIStroke") fovKnobStroke.Color = Config.Theme.TabActive; fovKnobStroke.Thickness = 2; fovKnobStroke.Parent = fovKnob

    local FOVCircle = nil
    local FOVFrame = nil

    local function updateFOVSlider(val)
        val = math.clamp(val, FOV_MIN, FOV_MAX)
        Config.AimFOV = val
        local alpha = (val - FOV_MIN) / (FOV_MAX - FOV_MIN)
        fovFill.Size = UDim2.new(alpha, 0, 1, 0)
        fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
        fovValueLbl.Text = tostring(val)
        if FOVCircle and HasDrawing then pcall(function() FOVCircle.Radius = val end) end
        if FOVFrame then
            local d = math.floor(val * 2)
            FOVFrame.Size = UDim2.new(0, d, 0, d)
        end
    end

    local fovDragging = false
    local function fFI(input)
        local absPos = fovTrack.AbsolutePosition.X
        local absSize = fovTrack.AbsoluteSize.X
        if absSize <= 0 then return end
        local alpha = math.clamp((input.Position.X - absPos) / absSize, 0, 1)
        updateFOVSlider(math.floor(FOV_MIN + alpha * (FOV_MAX - FOV_MIN) + 0.5))
    end
    fovTrack.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then fovDragging = true; fFI(input) end
    end)
    fovKnob.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then fovDragging = true end
    end)
    sC(UserInputService.InputChanged, function(input)
        if fovDragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then fFI(input) end
    end)
    sC(UserInputService.InputEnded, function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            if fovDragging then fovDragging = false; sCfg() end
        end
    end)

    local sliderSec = Instance.new("Frame") sliderSec.Size = UDim2.new(1, 0, 0, 65); sliderSec.BackgroundTransparency = 1; sliderSec.Parent = ContentConfig
    local sliderLbl = Instance.new("TextLabel") sliderLbl.Size = UDim2.new(1, 0, 0, 18); sliderLbl.Font = Enum.Font.GothamBold; sliderLbl.TextSize = 11; sliderLbl.TextColor3 = Config.Theme.TextSecondary; sliderLbl.Text = string.format(_L.distEsp, tostring(Config.MaxNormalDistance)); sliderLbl.TextXAlignment = Enum.TextXAlignment.Left; sliderLbl.BackgroundTransparency = 1; sliderLbl.Parent = sliderSec

    local sliderCont = Instance.new("Frame") sliderCont.Size = UDim2.new(1, 0, 0, 32); sliderCont.Position = UDim2.new(0, 0, 0, 22); sliderCont.BackgroundColor3 = Config.Theme.TabInactive; sliderCont.Parent = sliderSec
    Instance.new("UICorner", sliderCont).CornerRadius = UDim.new(0, 6)

    local sliderBar = Instance.new("Frame") sliderBar.Size = UDim2.new(1, -20, 0, 6); sliderBar.Position = UDim2.new(0, 10, 0.5, -3); sliderBar.BackgroundColor3 = Color3.fromRGB(40, 35, 60); sliderBar.BorderSizePixel = 0; sliderBar.Parent = sliderCont
    Instance.new("UICorner", sliderBar).CornerRadius = UDim.new(0, 3)

    local sliderFill = Instance.new("Frame") sliderFill.BackgroundColor3 = Config.Theme.TabActive; sliderFill.BorderSizePixel = 0; sliderFill.Parent = sliderBar
    Instance.new("UICorner", sliderFill).CornerRadius = UDim.new(0, 3)

    local sliderBtn = Instance.new("TextButton") sliderBtn.Size = UDim2.new(0, 14, 0, 14); sliderBtn.BackgroundColor3 = Config.Theme.TextPrimary; sliderBtn.Text = ""; sliderBtn.Parent = sliderBar
    Instance.new("UICorner", sliderBtn).CornerRadius = UDim.new(1, 0)

    local minDist, maxDist = 100, 5000
    local sliderDrag = false
    local function updateSlider(val)
        local pct = math.clamp((val - minDist) / (maxDist - minDist), 0, 1)
        sliderBtn.Position = UDim2.new(pct, -7, 0.5, -7)
        sliderFill.Size = UDim2.new(pct, 0, 1, 0)
        sliderLbl.Text = string.format(_L.distEsp, tostring(val))
    end
    sliderBtn.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then sliderDrag = true end
    end)
    sC(UserInputService.InputEnded, function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            if sliderDrag then sliderDrag = false; sCfg() end
        end
    end)
    sC(UserInputService.InputChanged, function(input)
        if sliderDrag and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            local bSize = sliderBar.AbsoluteSize.X
            if bSize > 0 then
                local mX = input.Position.X - sliderBar.AbsolutePosition.X
                local pct = math.clamp(mX / bSize, 0, 1)
                local val = math.floor(minDist + (pct * (maxDist - minDist)))
                Config.MaxNormalDistance = val
                Config.MaxSpecialDistance = math.floor(val * 1.5)
                updateSlider(val)
            end
        end
    end)
    updateSlider(Config.MaxNormalDistance)

    modeController = cCCS(_L.aimMode, {
        {Label = _L.modeToggle, Value = "Toggle"},
        {Label = _L.modeFov, Value = "FOV"},
        {Label = _L.modeHold, Value = "Hold"}
    }, function(val) Config.AimMode = val end)

    smoothController = cCCS(_L.smooth, {
        {Label = _L.low, Value = "Bajo"},
        {Label = _L.mid, Value = "Medio"},
        {Label = _L.high, Value = "Alto"}
    }, function(val) Config.AimSmooth = val end)

    targetController = cCCS(_L.target, {
        {Label = _L.head, Value = "Cabeza"},
        {Label = _L.chest, Value = "Pecho"},
        {Label = _L.mixed, Value = "Mixto"}
    }, function(val) Config.AimTarget = val; State.lockedTarget = nil end)

    rpgController = cCCS(_L.rpgMode, {
        {Label = _L.rpgDuro, Value = "DURO"},
        {Label = _L.rpgNormal, Value = "Normal"},
        {Label = _L.rpgBacio, Value = "Bacio"}
    }, function(val) Config.RPGAimMode = val; State.lockedTarget = nil end)

    skelController = cCCS(_L.skel, {
        {Label = _L.off, Value = "Off"},
        {Label = _L.gold, Value = "Oro"},
        {Label = _L.white, Value = "Blanco"}
    }, function(val) 
        Config.SkeletonStyle = val 
        if val == "Off" then hideAllSkeletons() end
    end)

    legAuraController = cCCS(_L.legAura, {
        {Label = "On", Value = true},
        {Label = "Off", Value = false}
    }, function(val) Config.LegendaryAuraEnabled = val end)

    local bindSectionFrame = Instance.new("Frame") bindSectionFrame.Size = UDim2.new(1, 0, 0, 58); bindSectionFrame.BackgroundTransparency = 1; bindSectionFrame.Parent = ContentConfig
    local bindLbl = Instance.new("TextLabel") bindLbl.Size = UDim2.new(1, 0, 0, 18); bindLbl.Font = Enum.Font.GothamBold; bindLbl.TextSize = 11; bindLbl.TextColor3 = Config.Theme.TextSecondary; bindLbl.Text = _L.binds; bindLbl.TextXAlignment = Enum.TextXAlignment.Left; bindLbl.BackgroundTransparency = 1; bindLbl.Parent = bindSectionFrame

    local bindContainer = Instance.new("Frame") bindContainer.Size = UDim2.new(1, 0, 0, 32); bindContainer.Position = UDim2.new(0, 0, 0, 22); bindContainer.BackgroundTransparency = 1; bindContainer.Parent = bindSectionFrame
    local bindLayout = Instance.new("UIListLayout") bindLayout.FillDirection = Enum.FillDirection.Horizontal; bindLayout.Padding = UDim.new(0, 6); bindLayout.Parent = bindContainer

    local bindButtons = {}
    local bindActions = {"ToggleMenu", "Aimbot", "InvView"}
    local bindLabels = {ToggleMenu = "Menu", Aimbot = "Aim", InvView = "Inv"}
    for _, action in ipairs(bindActions) do
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(0.33, -4, 1, 0); btn.Font = Enum.Font.GothamBold; btn.TextSize = 10
        btn.BackgroundColor3 = Config.Theme.TabInactive; btn.TextColor3 = Config.Theme.TextPrimary; btn.Parent = bindContainer
        Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)
        bindButtons[action] = btn
        btn.MouseButton1Click:Connect(function()
            if State.isBinding then return end
            State.isBinding = action; btn.Text = _L.pressKey; btn.BackgroundColor3 = Config.Theme.PinActive
        end)
    end

    local function uBUT()
        for action, btn in pairs(bindButtons) do
            if State.isBinding ~= action then
                btn.Text = bindLabels[action] .. ": [" .. Config.Binds[action].Name .. "]"
                btn.BackgroundColor3 = Config.Theme.TabInactive
                btn.TextColor3 = Config.Theme.TextPrimary
            end
        end
    end

    local function sCU()
        if modeController then modeController.setValue(Config.AimMode) end
        if smoothController then smoothController.setValue(Config.AimSmooth) end
        if targetController then targetController.setValue(Config.AimTarget) end
        if rpgController then rpgController.setValue(Config.RPGAimMode) end
        if skelController then skelController.setValue(Config.SkeletonStyle) end
        if legAuraController then legAuraController.setValue(Config.LegendaryAuraEnabled) end
        updateSlider(Config.MaxNormalDistance)
        updateFOVSlider(Config.AimFOV)
        uBUT()
        uRPG()
    end

    sCfg = function()
        if not (type(writefile) == "function") then return false end
        local saveData = {
            AimTarget = Config.AimTarget, RPGAimEnabled = Config.RPGAimEnabled, RPGAimMode = Config.RPGAimMode, AimSmooth = Config.AimSmooth, AimMode = Config.AimMode,
            AimFOV = Config.AimFOV, ShowFOV = Config.ShowFOV, SkeletonStyle = Config.SkeletonStyle, LegendaryAuraEnabled = Config.LegendaryAuraEnabled, MaxNormalDistance = Config.MaxNormalDistance, AutoExecute = Config.AutoExecute,
            Binds = {ToggleMenu = Config.Binds.ToggleMenu.Name, Aimbot = Config.Binds.Aimbot.Name, InvView = Config.Binds.InvView.Name},
            Toggles = {aimEnabled = State.aimEnabled, espEnabled = State.espEnabled, invViewEnabled = State.invViewEnabled, tracersEnabled = State.tracersEnabled}
        }
        local success, encoded = pcall(function() return HttpService:JSONEncode(saveData) end)
        if success and encoded then pcall(function() writefile(CONFIG_FILE, encoded) end) return true end
        return false
    end

    lCfg = function()
        if not (type(readfile) == "function" and type(isfile) == "function") or not isfile(CONFIG_FILE) then return false end
        local success, content = pcall(function() return readfile(CONFIG_FILE) end)
        if not success or not content then return false end
        local decodeSuccess, decoded = pcall(function() return HttpService:JSONDecode(content) end)
        if not decodeSuccess or type(decoded) ~= "table" then return false end
        if decoded.AimTarget ~= nil then Config.AimTarget = decoded.AimTarget end
        if decoded.RPGAimEnabled ~= nil then Config.RPGAimEnabled = decoded.RPGAimEnabled end
        if decoded.RPGAimMode ~= nil then Config.RPGAimMode = decoded.RPGAimMode end
        if decoded.AimSmooth ~= nil then Config.AimSmooth = decoded.AimSmooth end
        if decoded.AimMode ~= nil then Config.AimMode = decoded.AimMode end
        if decoded.AimFOV ~= nil then Config.AimFOV = tonumber(decoded.AimFOV) or Config.AimFOV end
        if decoded.SkeletonStyle ~= nil then Config.SkeletonStyle = decoded.SkeletonStyle end
        if decoded.LegendaryAuraEnabled ~= nil then Config.LegendaryAuraEnabled = decoded.LegendaryAuraEnabled end
        if decoded.MaxNormalDistance ~= nil then
            Config.MaxNormalDistance = decoded.MaxNormalDistance
            Config.MaxSpecialDistance = math.floor(decoded.MaxNormalDistance * 1.5)
        end
        if type(decoded.Binds) == "table" then
            for action, keyName in pairs(decoded.Binds) do
                if Config.Binds[action] and Enum.KeyCode[keyName] then Config.Binds[action] = Enum.KeyCode[keyName] end
            end
        end
        if type(decoded.Toggles) == "table" then
            if decoded.Toggles.aimEnabled ~= nil then State.aimEnabled = decoded.Toggles.aimEnabled end
            if decoded.Toggles.espEnabled ~= nil then State.espEnabled = decoded.Toggles.espEnabled end
            if decoded.Toggles.invViewEnabled ~= nil then State.invViewEnabled = decoded.Toggles.invViewEnabled end
            if decoded.Toggles.tracersEnabled ~= nil then State.tracersEnabled = decoded.Toggles.tracersEnabled end
        end
        sCU(); uMB()
        return true
    end
    sCU()

    saveBtn.MouseButton1Click:Connect(function()
        if sCfg() then
            saveBtn.Text = _L.saved; saveBtn.BackgroundColor3 = Config.Theme.TeamActive; saveBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
            task.delay(1.5, function() saveBtn.Text = _L.saveCfg; saveBtn.BackgroundColor3 = Config.Theme.TabInactive; saveBtn.TextColor3 = Config.Theme.TextPrimary end)
        end
    end)
    loadBtn.MouseButton1Click:Connect(function()
        if lCfg() then
            loadBtn.Text = _L.loaded; loadBtn.BackgroundColor3 = Config.Theme.TeamActive; loadBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
            task.delay(1.5, function() loadBtn.Text = _L.loadCfg; loadBtn.BackgroundColor3 = Config.Theme.TabInactive; loadBtn.TextColor3 = Config.Theme.TextPrimary end)
        end
    end)

    local function gMRP()
        local char = LocalPlayer.Character
        if char then
            local hum = char:FindFirstChildOfClass("Humanoid")
            if hum and hum.SeatPart then return hum.SeatPart.Position end
            local root = char:FindFirstChild("HumanoidRootPart")
            if root then return root.Position end
        end
        return Camera.CFrame.Position
    end

    local function rPL()
        local activePlayers, playerList = {}, {}
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer then activePlayers[player.Name] = true; table.insert(playerList, player) end
        end
        for name, frame in pairs(PlayerRowCache) do
            if not activePlayers[name] then frame:Destroy(); PlayerRowCache[name] = nil end
        end
        table.sort(playerList, function(a, b)
            local aPinned = State.pinnedPlayers[a.Name] and 1 or 0
            local bPinned = State.pinnedPlayers[b.Name] and 1 or 0
            if aPinned ~= bPinned then return aPinned > bPinned end
            return a.Name < b.Name
        end)
        for order, player in ipairs(playerList) do
            local isPinned, isTeam = State.pinnedPlayers[player.Name], State.teamPlayers[player.Name]
            local playerWrapper = PlayerRowCache[player.Name]
            if not playerWrapper then
                playerWrapper = Instance.new("Frame")
                playerWrapper.Size = UDim2.new(1, -6, 0, 40)
                Instance.new("UICorner", playerWrapper).CornerRadius = UDim.new(0, 6)
                
                local userBtn = Instance.new("TextLabel")
                userBtn.Name = "UserBtn"; userBtn.Size = UDim2.new(1, -120, 1, 0); userBtn.Position = UDim2.new(0, 10, 0, 0)
                userBtn.BackgroundTransparency = 1; userBtn.Font = Enum.Font.GothamBold; userBtn.TextSize = 11; userBtn.TextXAlignment = Enum.TextXAlignment.Left; userBtn.Parent = playerWrapper
                
                local teamBtn = Instance.new("TextButton")
                teamBtn.Name = "TeamBtn"; teamBtn.Size = UDim2.new(0, 50, 0, 24); teamBtn.Position = UDim2.new(1, -105, 0.5, -12)
                teamBtn.Font = Enum.Font.GothamBold; teamBtn.TextSize = 9; teamBtn.TextColor3 = Config.Theme.TextPrimary
                Instance.new("UICorner", teamBtn).CornerRadius = UDim.new(0, 4); teamBtn.Parent = playerWrapper
                
                local pinBtn = Instance.new("TextButton")
                pinBtn.Name = "PinBtn"; pinBtn.Size = UDim2.new(0, 45, 0, 24); pinBtn.Position = UDim2.new(1, -50, 0.5, -12)
                pinBtn.Font = Enum.Font.GothamBold; pinBtn.TextSize = 9; pinBtn.TextColor3 = Config.Theme.TextPrimary
                Instance.new("UICorner", pinBtn).CornerRadius = UDim.new(0, 4); pinBtn.Parent = playerWrapper
                
                teamBtn.MouseButton1Click:Connect(function() State.teamPlayers[player.Name] = not State.teamPlayers[player.Name] or nil; rPL(); sCfg() end)
                pinBtn.MouseButton1Click:Connect(function()
                    if State.pinnedPlayers[player.Name] then State.pinnedPlayers[player.Name] = nil; State.autoPinned[player.Name] = nil else State.pinnedPlayers[player.Name] = true end
                    rPL(); sCfg()
                end)
                PlayerRowCache[player.Name] = playerWrapper
                playerWrapper.Parent = scroll
            end
            playerWrapper.LayoutOrder = order
            playerWrapper.BackgroundColor3 = isPinned and Config.Theme.PlayerRowPinned or Config.Theme.PlayerRow
            local userBtn = playerWrapper:FindFirstChild("UserBtn")
            local teamBtn = playerWrapper:FindFirstChild("TeamBtn")
            local pinBtn = playerWrapper:FindFirstChild("PinBtn")
            if userBtn then
                userBtn.TextColor3 = isTeam and Config.Theme.EspTeam or (isPinned and Config.Theme.EspPinned or Config.Theme.TextPrimary)
                userBtn.Text = (isTeam and ("[" .. _L.ally .. "] ") or (isPinned and ("[" .. _L.targetTag .. "] ") or "")) .. player.DisplayName
            end
            if teamBtn then
                teamBtn.BackgroundColor3 = isTeam and Config.Theme.TeamActive or Config.Theme.PinInactive
                teamBtn.Text = isTeam and _L.noTeam or _L.team; teamBtn.TextColor3 = isTeam and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
            end
            if pinBtn then
                pinBtn.BackgroundColor3 = isPinned and Config.Theme.PinActive or Config.Theme.PinInactive
                pinBtn.Text = isPinned and _L.unpin or _L.pin; pinBtn.TextColor3 = isPinned and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
            end
        end
    end

    local function gRC(rarity)
        local colors = {Common = Color3.fromRGB(0, 255, 100), Rare = Color3.fromRGB(0, 150, 255), Epic = Color3.fromRGB(180, 50, 255), Legendary = Color3.fromRGB(255, 200, 0)}
        return colors[rarity] or Color3.fromRGB(255, 255, 255)
    end

    local function mTN(tool)
        if not tool then return "Unknown" end
        local name = tool.Name
        if ToolNameCache[name] then return ToolNameCache[name] end
        local handle = tool:FindFirstChild("Handle")
        if not handle then ToolNameCache[name] = name; return name end
        local names = {}
        for _, child in ipairs(handle:GetChildren()) do names[child.Name] = true end
        for _, source in ipairs({ReplicatedStorage:FindFirstChild("Items"), StarterPack}) do
            if source then
                for _, item in ipairs(source:GetDescendants()) do
                    if item:IsA("Tool") and item:FindFirstChild("Handle") then
                        local matches = true
                        for childName in pairs(names) do if not item.Handle:FindFirstChild(childName) then matches = false; break end end
                        if matches then ToolNameCache[name] = item.Name; return item.Name end
                    end
                end
            end
        end
        ToolNameCache[name] = name; return name
    end

    local function gPT(player)
        local now = tick()
        if LastToolScan[player.Name] and (now - LastToolScan[player.Name].time < 1.5) then
            return LastToolScan[player.Name].tools
        end
        local tools = {}
        if not player then return tools end
        local hasLegendary = false
        local backpack = player:FindFirstChildOfClass("Backpack")
        local character = player.Character
        local function scanContainer(container)
            if not container then return end
            for _, tool in ipairs(container:GetChildren()) do
                if tool:IsA("Tool") then
                    local realName = mTN(tool)
                    local rarity = tool:GetAttribute("RarityName") or "Common"
                    if rarity == "Legendary" then hasLegendary = true end
                    table.insert(tools, {name = realName, rarity = rarity, equipped = (container == character)})
                end
            end
        end
        scanContainer(backpack); scanContainer(character)
        if hasLegendary then
            if not State.pinnedPlayers[player.Name] then
                State.pinnedPlayers[player.Name] = true
                State.autoPinned[player.Name] = true
                task.spawn(rPL)
            end
        else
            if State.autoPinned[player.Name] then
                State.pinnedPlayers[player.Name] = nil
                State.autoPinned[player.Name] = nil
                task.spawn(rPL)
            end
        end
        LastToolScan[player.Name] = {time = now, tools = tools}
        return tools
    end

    local function gOME(player)
        if MasterObjects[player.Name] then return MasterObjects[player.Name] end
        local char = player.Character
        if not char then return nil end
        local head = char:FindFirstChild("Head")
        if not head then return nil end
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "BsMasterEsp"; billboard.Size = UDim2.new(0, 200, 0, 200); billboard.StudsOffset = Vector3.new(0, 3.8, 0); billboard.AlwaysOnTop = true; billboard.Parent = head
        local mainLayoutFrame = Instance.new("Frame")
        mainLayoutFrame.Size = UDim2.new(1, 0, 1, 0); mainLayoutFrame.BackgroundTransparency = 1; mainLayoutFrame.Parent = billboard
        
        local listLayout = Instance.new("UIListLayout")
        listLayout.FillDirection = Enum.FillDirection.Vertical; listLayout.SortOrder = Enum.SortOrder.LayoutOrder
        listLayout.Padding = UDim.new(0, 4); listLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center; listLayout.Parent = mainLayoutFrame
        
        local espLabel = Instance.new("TextLabel")
        espLabel.Name = "EspLabel"; espLabel.Size = UDim2.new(1, 0, 0, 55); espLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
        espLabel.BackgroundTransparency = 0.65; espLabel.Font = Enum.Font.GothamBold; espLabel.TextStrokeTransparency = 0.4; espLabel.LayoutOrder = 1
        Instance.new("UICorner", espLabel).CornerRadius = UDim.new(0, 5); espLabel.Parent = mainLayoutFrame
        
        local invContainer = Instance.new("Frame")
        invContainer.Name = "InvContainer"; invContainer.Size = UDim2.new(1, 0, 0, 120); invContainer.BackgroundTransparency = 1; invContainer.LayoutOrder = 2; invContainer.Parent = mainLayoutFrame
        local invLayout = Instance.new("UIListLayout")
        invLayout.FillDirection = Enum.FillDirection.Vertical; invLayout.SortOrder = Enum.SortOrder.LayoutOrder
        invLayout.Padding = UDim.new(0, 2); invLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center; invLayout.Parent = invContainer
        
        MasterObjects[player.Name] = {Gui = billboard, EspLabel = espLabel, InvContainer = invContainer}
        return MasterObjects[player.Name]
    end

    local function rME(player)
        local master = MasterObjects[player.Name]
        if master then
            if master.Gui then master.Gui:Destroy() end
            MasterObjects[player.Name] = nil; LastInventoryState[player] = nil
        end
        hSk(player)
    end

    local function uV()
        if not State.alive then return end
        local myPosition = gMRP()
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer then
                local char = player.Character
                if char then
                    local head, root, hum = char:FindFirstChild("Head"), char:FindFirstChild("HumanoidRootPart"), char:FindFirstChildOfClass("Humanoid")
                    if head and root and hum then
                        local isPinned, isTeam = State.pinnedPlayers[player.Name], State.teamPlayers[player.Name]
                        local isLocked = (State.lockedTarget == player)
                        local isLegendaryOwner = State.autoPinned[player.Name]
                        local showLegAura = Config.LegendaryAuraEnabled and isLegendaryOwner
                        local distance = math.floor((root.Position - myPosition).Magnitude)
                        local maxDist = (isPinned or isTeam) and Config.MaxSpecialDistance or Config.MaxNormalDistance
                        
                        if hum.Health > 0 and distance <= maxDist then
                            local master = gOME(player)
                            if master and master.Gui and master.Gui.Parent == head then
                                master.Gui.Enabled = true
                                local textScale = math.clamp(12 - (distance / 400), 8.5, 12)
                                if State.espEnabled then
                                    master.EspLabel.Visible = true
                                    if isLocked then
                                        master.EspLabel.TextColor3 = Color3.fromRGB(255, 30, 30)
                                    else
                                        master.EspLabel.TextColor3 = isTeam and Config.Theme.EspTeam or (isPinned and Config.Theme.EspPinned or Config.Theme.EspNormal)
                                    end
                                    master.EspLabel.TextSize = textScale
                                    local tagPrefix = isLocked and ("[" .. _L.aiming .. "]\n") or (isTeam and ("[" .. _L.ally .. "]\n") or (isPinned and ("[" .. _L.targetTag .. "]\n") or ""))
                                    master.EspLabel.Text = string.format("%s%s\n%d studs | %d HP", tagPrefix, player.DisplayName, distance, math.floor(hum.Health))
                                else
                                    master.EspLabel.Visible = false
                                end
                                if State.invViewEnabled then
                                    master.InvContainer.Visible = true
                                    local tools = gPT(player)
                                    local inventoryString = ""
                                    for _, toolData in ipairs(tools) do inventoryString = inventoryString .. toolData.name .. toolData.rarity .. tostring(toolData.equipped) end
                                    if LastInventoryState[player] ~= inventoryString then
                                        LastInventoryState[player] = inventoryString
                                        for _, child in ipairs(master.InvContainer:GetChildren()) do if child:IsA("TextLabel") then child:Destroy() end end
                                        for i, toolData in ipairs(tools) do
                                            local line = Instance.new("TextLabel")
                                            line.Size = UDim2.new(0, 145, 0, 14); line.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
                                            line.BackgroundTransparency = 0.7; line.Font = Enum.Font.GothamBold; line.TextStrokeTransparency = 0.5
                                            local equipTag = toolData.equipped and "→ " or ""
                                            line.Text = equipTag .. toolData.name .. " "; line.TextColor3 = gRC(toolData.rarity); line.LayoutOrder = i
                                            Instance.new("UICorner", line).CornerRadius = UDim.new(0, 4)
                                            if toolData.equipped then line.BackgroundColor3 = Color3.fromRGB(45, 15, 25) end
                                            line.Parent = master.InvContainer
                                        end
                                    end
                                    for _, child in ipairs(master.InvContainer:GetChildren()) do if child:IsA("TextLabel") then child.TextSize = textScale end end
                                else
                                    master.InvContainer.Visible = false
                                end
                            else
                                rME(player)
                            end

                            if isTeam or isLocked or showLegAura then
                                local hl = char:FindFirstChild("BsAura")
                                if not hl then
                                    hl = Instance.new("Highlight")
                                    hl.Name = "BsAura"; hl.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                                    hl.OutlineColor = Color3.fromRGB(255, 255, 255); hl.Parent = char
                                end
                                if isTeam then
                                    hl.FillColor = Color3.fromRGB(0, 255, 140)
                                elseif isLocked then
                                    hl.FillColor = Color3.fromRGB(255, 0, 0)
                                else
                                    hl.FillColor = Color3.fromRGB(255, 215, 0)
                                end
                                hl.FillTransparency = 0.35; hl.OutlineTransparency = 0
                            else
                                local hl = char:FindFirstChild("BsAura")
                                if hl then hl:Destroy() end
                            end
                        else
                            rME(player)
                            local hl = char:FindFirstChild("BsAura")
                            if hl then hl:Destroy() end
                        end
                    else
                        rME(player)
                    end
                else
                    rME(player)
                end
            else
                rME(player)
            end
        end
    end

    if HasDrawing then
        pcall(function()
            FOVCircle = Drawing.new("Circle")
            FOVCircle.Thickness = 1.5; FOVCircle.NumSides = 60; FOVCircle.Filled = false; FOVCircle.Transparency = 1
            FOVCircle.Visible = false
        end)
    end

    do
        local initialDiam = math.floor(Config.AimFOV * 2)
        FOVFrame = Instance.new("Frame")
        FOVFrame.Name = "HCP_FOV_Circle"
        FOVFrame.AnchorPoint = Vector2.new(0.5, 0.5)
        FOVFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
        FOVFrame.Size = UDim2.new(0, initialDiam, 0, initialDiam)
        FOVFrame.BackgroundTransparency = 1
        FOVFrame.Visible = (Config.ShowFOV and Config.AimMode == "FOV")
        FOVFrame.ZIndex = 50
        FOVFrame.Parent = gui

        Instance.new("UICorner", FOVFrame).CornerRadius = UDim.new(1, 0)
        local fovStroke = Instance.new("UIStroke") fovStroke.Name = "Stroke"; fovStroke.Thickness = 1.5; fovStroke.Color = Config.Theme.FOVNormal; fovStroke.Transparency = 0; fovStroke.Parent = FOVFrame
    end

    local function gIPN(targetMode, char)
        if not char then return nil end
        local head = char:FindFirstChild("Head")
        local upperTorso = char:FindFirstChild("UpperTorso")
        local torso = upperTorso or char:FindFirstChild("Torso")
        local hum = char:FindFirstChildOfClass("Humanoid")

        if targetMode == "Pecho" then return torso and torso.Name or (head and "Head" or nil) end
        if targetMode == "Cabeza" then return head and "Head" or (torso and torso.Name or nil) end

        if targetMode == "Mixto" then
            if hum and hum.Health <= 35 then return head and "Head" or (torso and torso.Name or nil) end
            if math.random() < 0.82 and torso then return torso.Name end
            return head and "Head" or (torso and torso.Name or nil)
        end

        return torso and torso.Name or (head and "Head" or nil)
    end

    local function gCT()
        if Config.AimMode == "FOV" or Config.AimMode == "Hold" then
            local closest, minDist = nil, Config.AimFOV
            local center = Camera.ViewportSize / 2
            local current = State.lockedTarget
            local currentDist = math.huge
            for _, plr in ipairs(Players:GetPlayers()) do
                if plr ~= LocalPlayer and not State.teamPlayers[plr.Name] then
                    local char = plr.Character
                    if char then
                        local hum = char:FindFirstChildOfClass("Humanoid")
                        if hum and hum.Health > 0 then
                            local partName = gIPN(Config.AimTarget, char)
                            local part = partName and char:FindFirstChild(partName)
                            if part and part:IsA("BasePart") then
                                local pos, onScreen = Camera:WorldToViewportPoint(part.Position)
                                if onScreen then
                                    local dist = (Vector2.new(pos.X, pos.Y) - center).Magnitude
                                    if dist < minDist then minDist = dist; closest = plr end
                                    if current and plr == current then currentDist = dist end
                                end
                            end
                        end
                    end
                end
            end
            if current then
                local char = current.Character
                local hum = char and char:FindFirstChildOfClass("Humanoid")
                if State.teamPlayers[current.Name] or not char or not hum or hum.Health <= 0 or currentDist > Config.AimFOV then
                    State.lockedTarget = nil; current = nil
                end
            end
            if closest then
                if not current then State.lockedTarget = closest
                elseif closest ~= current and minDist < (currentDist * 0.72) then State.lockedTarget = closest end
            else
                State.lockedTarget = nil
            end
            return State.lockedTarget
        end
        local locked = State.lockedTarget
        if locked then
            local char = locked.Character
            local hum = char and char:FindFirstChildOfClass("Humanoid")
            if State.teamPlayers[locked.Name] or not char or not hum or hum.Health <= 0 then State.lockedTarget = nil; locked = nil end
        end
        if locked then return locked end
        local closest, minDist = nil, Config.AimFOV
        local center = Camera.ViewportSize / 2
        for _, plr in ipairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and not State.teamPlayers[plr.Name] then
                local char = plr.Character
                if char then
                    local hum = char:FindFirstChildOfClass("Humanoid")
                    if hum and hum.Health > 0 then
                        local partName = gIPN(Config.AimTarget, char)
                        local part = partName and char:FindFirstChild(partName)
                        if part and part:IsA("BasePart") then
                            local pos, onScreen = Camera:WorldToViewportPoint(part.Position)
                            if onScreen then
                                local dist = (Vector2.new(pos.X, pos.Y) - center).Magnitude
                                if dist < minDist then minDist = dist; closest = plr end
                            end
                        end
                    end
                end
            end
        end
        State.lockedTarget = closest
        return closest
    end

    task.spawn(function()
        while State.alive do
            uV()
            task.wait(0.033)
        end
    end)

    sC(RunService.RenderStepped, function(dt)
        if State.espEnabled and Config.SkeletonStyle ~= "Off" then
            local myPos = gMRP()
            for _, player in ipairs(Players:GetPlayers()) do
                if player ~= LocalPlayer and player.Character then
                    local root = player.Character:FindFirstChild("HumanoidRootPart")
                    local hum = player.Character:FindFirstChildOfClass("Humanoid")
                    if root and hum and hum.Health > 0 then
                        local dist = (root.Position - myPos).Magnitude
                        local maxD = (State.pinnedPlayers[player.Name] or State.teamPlayers[player.Name]) and Config.MaxSpecialDistance or Config.MaxNormalDistance
                        if dist <= maxD then uSE(player, player.Character) else hSk(player) end
                    else hSk(player) end
                end
            end
        else
            hideAllSkeletons()
        end

        local showFov = (Config.ShowFOV and Config.AimMode == "FOV")
        local fovCol = State.lockedTarget and Config.Theme.FOVLocked or Config.Theme.FOVNormal
        local fovDiam = math.floor(Config.AimFOV * 2)

        if FOVCircle and HasDrawing then
            pcall(function()
                FOVCircle.Radius = Config.AimFOV
                FOVCircle.Position = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)
                FOVCircle.Color = fovCol
                FOVCircle.Visible = showFov
            end)
        end

        if FOVFrame then
            FOVFrame.Size = UDim2.new(0, fovDiam, 0, fovDiam)
            FOVFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
            FOVFrame.Visible = showFov
            local st = FOVFrame:FindFirstChild("Stroke")
            if st then st.Color = fovCol end
        end
    end)

    RunService:BindToRenderStep("BlockSpinAimbot", Enum.RenderPriority.Camera.Value + 1, function(dt)
        if not State.alive then return end
        local shouldAim = false
        if Config.AimMode == "Toggle" then shouldAim = State.aimEnabled
        elseif Config.AimMode == "FOV" then shouldAim = State.holdingAimTrigger or State.aimEnabled
        elseif Config.AimMode == "Hold" then shouldAim = State.holdingAimTrigger end
        if not shouldAim then return end
        
        local target = gCT()
        if target and target.Character then
            local partName = gIPN(Config.AimTarget, target.Character)
            local part = partName and target.Character:FindFirstChild(partName)
            if part and part:IsA("BasePart") then
                local camPos = Camera.CFrame.Position
                local targetPos = part.Position

                trackSample(target)

                if Config.RPGAimEnabled then
                    local rpgMode = Config.RPGAimMode or "Normal"
                    local rootPart = target.Character:FindFirstChild("HumanoidRootPart") or part
                    local rawVel = rootPart.AssemblyLinearVelocity or rootPart.Velocity or Vector3.zero
                    local horizontalVel = Vector3.new(rawVel.X, 0, rawVel.Z)
                    local myRoot = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                    local originXZ = myRoot and Vector3.new(myRoot.Position.X, 0, myRoot.Position.Z) or Vector3.new(camPos.X, 0, camPos.Z)
                    local targetXZ = Vector3.new(rootPart.Position.X, 0, rootPart.Position.Z)
                    local distanceXZ = (targetXZ - originXZ).Magnitude
                    local pingSec = getPingInSeconds()
                    local rocketSpeed = Config.RPGRocketSpeed or 260

                    local blendVel, accel, speed, confidence = analyzeMotion()
                    local predVel = blendVel
                    if confidence < 0.35 or predVel.Magnitude < 0.5 then predVel = horizontalVel end

                    local toTarget = targetXZ - originXZ
                    local movingAway = false
                    local chaseFactor = 1.0
                    if predVel.Magnitude > 2.5 and toTarget.Magnitude > 8 then
                        local awayDot = toTarget.Unit:Dot(predVel.Unit)
                        if awayDot > 0.25 then
                            movingAway = true
                            chaseFactor = 1.35 + math.clamp(awayDot * 0.55, 0, 0.55) + math.clamp(speed / 90, 0, 0.45)
                        end
                    end

                    if rpgMode == "DURO" then
                        if distanceXZ < 90 then
                            local leadClose = movingAway and (predVel * (0.18 + pingSec * 0.6) * chaseFactor) or Vector3.zero
                            local aimPos = rootPart.Position + leadClose
                            local groundPoint = getGroundPosition(aimPos, target.Character)
                            targetPos = Vector3.new(aimPos.X, groundPoint.Y, aimPos.Z)
                        else
                            local travelTime = distanceXZ / math.max(rocketSpeed, 120)
                            local distFactor = 1 + math.clamp((distanceXZ - 85) / 900, 0, 0.28)
                            local pingBoost = pingSec * (1.15 + math.clamp(distanceXZ / 700, 0, 0.35))

                            local timeToImpact = math.clamp((travelTime * distFactor * chaseFactor) + pingBoost, 0.05, 2.1)
                            local futurePos = rootPart.Position + (predVel * timeToImpact) + (accel * (0.28 * timeToImpact * timeToImpact) * confidence)
                            local dist2 = (Vector3.new(futurePos.X, 0, futurePos.Z) - originXZ).Magnitude
                            local t2 = math.clamp((dist2 / math.max(rocketSpeed, 120)) * distFactor * chaseFactor + pingBoost, 0.05, 2.1)
                            local tFinal = (timeToImpact * 0.6 + t2 * 0.4)

                            futurePos = rootPart.Position + (predVel * tFinal) + (accel * (0.22 * tFinal * tFinal) * confidence)

                            if movingAway then
                                local extraLead = predVel.Unit * (4.5 + math.clamp(distanceXZ / 18, 0, 14) * chaseFactor)
                                futurePos = futurePos + Vector3.new(extraLead.X, 0, extraLead.Z)
                            end

                            local leadVec = Vector3.new(futurePos.X - rootPart.Position.X, 0, futurePos.Z - rootPart.Position.Z)
                            local maxLead = (movingAway and 11 or 7) + math.clamp(distanceXZ / 20, 0, movingAway and 18 or 13)
                            if leadVec.Magnitude > maxLead then
                                leadVec = leadVec.Unit * maxLead
                                futurePos = rootPart.Position + Vector3.new(leadVec.X, 0, leadVec.Z)
                            end
                            local groundPoint = getGroundPosition(futurePos, target.Character)
                            targetPos = Vector3.new(futurePos.X, groundPoint.Y, futurePos.Z)
                        end
                    elseif rpgMode == "Bacio" then
                        if distanceXZ < 70 then
                            local leadClose = movingAway and (predVel * (0.12 + pingSec * 0.4)) or Vector3.zero
                            targetPos = Vector3.new(rootPart.Position.X + leadClose.X, rootPart.Position.Y - 1.5, rootPart.Position.Z + leadClose.Z)
                        else
                            local leadT = (pingSec * 1.2 + math.clamp(distanceXZ / 750, 0.06, 0.38)) * chaseFactor
                            local futurePos = rootPart.Position + (predVel * leadT)
                            if movingAway then futurePos = futurePos + (predVel.Unit * (3 + math.clamp(distanceXZ / 30, 0, 8))) end
                            targetPos = Vector3.new(futurePos.X, rootPart.Position.Y - 1.5, futurePos.Z)
                        end
                    end
                end

                if (targetPos - camPos).Magnitude < 0.5 then return end
                local desired = CFrame.new(camPos, targetPos)
                local ok, x, y = pcall(function() return desired:ToEulerAnglesYXZ() end)
                if ok then
                    x = math.clamp(x, math.rad(-80), math.rad(80))
                    desired = CFrame.new(camPos) * CFrame.fromEulerAnglesYXZ(x, y, 0)
                end

                local alpha = 1
                if Config.RPGAimEnabled then
                    if Config.RPGAimMode == "DURO" then alpha = 1
                    elseif Config.RPGAimMode == "Normal" then alpha = 1 - math.exp(-45 * dt)
                    else alpha = 1 - math.exp(-18 * dt) end
                else
                    if Config.AimSmooth == "Bajo" or Config.AimSmooth == "Duro" then alpha = 1
                    elseif Config.AimSmooth == "Medio" then alpha = 1 - math.exp(-45 * dt)
                    else alpha = 1 - math.exp(-18 * dt) end
                end

                if alpha >= 1 then Camera.CFrame = desired
                else Camera.CFrame = Camera.CFrame:Lerp(desired, math.clamp(alpha, 0, 1)) end
            end
        end
    end)

    local tracerLoopRunning = false

    sC(UserInputService.InputBegan, function(input, gpe)
        if State.isBinding then
            if not gpe and input.UserInputType == Enum.UserInputType.Keyboard then
                local action = State.isBinding
                Config.Binds[action] = input.KeyCode; State.isBinding = nil; sCU(); sCfg()
            end
            return
        end

        if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == Config.Binds.GamepadAim then 
            State.holdingAimTrigger = true 
        end

        if not gpe then
            if input.KeyCode == Config.Binds.ToggleMenu then
                MainFrame.Visible = not MainFrame.Visible
            elseif input.KeyCode == Config.Binds.Aimbot or input.KeyCode == Config.Binds.GamepadToggle then
                State.aimEnabled = not State.aimEnabled; if not State.aimEnabled then State.lockedTarget = nil end; uMB(); sCfg()
            elseif input.KeyCode == Config.Binds.InvView then
                State.invViewEnabled = not State.invViewEnabled; uMB(); sCfg()
            end

            if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
                State.isShooting = true
                if State.tracersEnabled and not tracerLoopRunning then
                    tracerLoopRunning = true
                    task.spawn(function()
                        while State.isShooting and State.tracersEnabled and State.alive do
                            local myChar = LocalPlayer.Character
                            if myChar and myChar:FindFirstChildOfClass("Tool") then
                                local startPos = getMuzzlePosition()
                                local endPos = nil
                                
                                if State.lockedTarget and State.lockedTarget.Character then
                                    local partName = gIPN(Config.AimTarget, State.lockedTarget.Character)
                                    local part = partName and State.lockedTarget.Character:FindFirstChild(partName)
                                    if part then endPos = part.Position end
                                end
                                
                                if not endPos then
                                    local mouseRay = Camera:ViewportPointToRay(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)
                                    tracerRayParams.FilterDescendantsInstances = {myChar}
                                    local rayResult = workspace:Raycast(mouseRay.Origin, mouseRay.Direction * 2000, tracerRayParams)
                                    if rayResult then endPos = rayResult.Position
                                    else endPos = mouseRay.Origin + (mouseRay.Direction * 2000) end
                                end
                                
                                drawBulletTracer(startPos, endPos)
                            end
                            task.wait(0.12)
                        end
                        tracerLoopRunning = false
                    end)
                end
            end
        end
    end)

    sC(UserInputService.InputEnded, function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then State.isShooting = false end
        if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == Config.Binds.GamepadAim then
            State.holdingAimTrigger = false; State.lockedTarget = nil; trackClear()
        end
    end)

    local dragging = false
    local dragStart = Vector3.zero
    local startPos = UDim2.new()
    header.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true; dragStart = input.Position; startPos = MainFrame.Position
        end
    end)
    sC(UserInputService.InputChanged, function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            local delta = input.Position - dragStart
            MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
    sC(UserInputService.InputEnded, function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then dragging = false end
    end)

    local function fullCleanup()
        State.alive = false
        pcall(function() RunService:UnbindFromRenderStep("BlockSpinAimbot") end)
        for _, conn in ipairs(State.connections) do pcall(function() conn:Disconnect() end) end
        table.clear(State.connections)

        if FOVCircle then pcall(function() FOVCircle:Remove() end) end
        if FOVFrame then pcall(function() FOVFrame:Destroy() end) end

        for _, p in ipairs(Players:GetPlayers()) do 
            rME(p)
            if p.Character then
                local hl = p.Character:FindFirstChild("BsAura")
                if hl then pcall(function() hl:Destroy() end) end
            end
        end

        for _, lines in pairs(SkelCache) do
            for _, l in pairs(lines) do if l then pcall(function() l:Remove() end) end end
        end
        table.clear(SkelCache)

        for _, obj in ipairs(workspace:GetChildren()) do
            if obj.Name == "HCP_Tracer" then pcall(function() obj:Destroy() end) end
        end

        pcall(function() gui:Destroy() end)
    end

    closeBtn.MouseButton1Click:Connect(fullCleanup)

    sC(Players.PlayerAdded, function(p) cAAT(p); rPL() end)
    sC(Players.PlayerRemoving, function(p)
        rME(p)
        State.teamPlayers[p.Name] = nil; State.pinnedPlayers[p.Name] = nil; State.autoPinned[p.Name] = nil
        if State.lockedTarget == p then State.lockedTarget = nil end
        local row = PlayerRowCache[p.Name]
        if row then pcall(function() row:Destroy() end); PlayerRowCache[p.Name] = nil end
        task.defer(rPL)
    end)

    for _, p in ipairs(Players:GetPlayers()) do if p ~= LocalPlayer then cAAT(p) end end
    rPL()
    task.spawn(lCfg)
    print("[Hermanos CP Unified] Cargado correctamente.")
end

local function s()
    _G.HCP_LANG = h and "en" or "es"
    print(o().requesting .. "...")
    local ok, err = pcall(runUnifiedScript)
    if not ok then warn("[HCP] Error al ejecutar script: " .. tostring(err)) end
end

local z = Instance.new("ScreenGui")
z.Name = "HermanosCPLoader_Premium"
z.IgnoreGuiInset = true
z.ResetOnSpawn = false
z.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
z.Parent = p()

local function A(B, C)
    if C then 
        B.BackgroundColor3 = Color3.fromRGB(0, 140, 220)
        B.TextColor3 = Color3.fromRGB(255, 255, 255)
    else 
        B.BackgroundColor3 = Color3.fromRGB(28, 28, 40)
        B.TextColor3 = Color3.fromRGB(160, 165, 180)
    end
end

local function D(E, F)
    local G = Instance.new("Frame")
    G.Size = UDim2.new(0, E, 0, F)
    G.Position = UDim2.new(0.5, -math.floor(E/2), 0.5, -math.floor(F/2))
    G.BackgroundColor3 = Color3.fromRGB(10, 10, 15)
    G.BorderSizePixel = 0
    G.ClipsDescendants = true
    G.Parent = z
    Instance.new("UICorner", G).CornerRadius = UDim.new(0, 12)
    local H = Instance.new("UIStroke")
    H.Color = Color3.fromRGB(0, 180, 255)
    H.Thickness = 1.5
    H.Transparency = 0.2
    H.Parent = G
    local I = Instance.new("UIGradient")
    I.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(15, 12, 28)),
        ColorSequenceKeypoint.new(0.5, Color3.fromRGB(8, 8, 12)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(5, 15, 20))
    })
    I.Rotation = 45
    I.Parent = G
    return G, H
end

local function J(K, L, M, N, O)
    local P = Instance.new("Frame")
    P.Size = UDim2.new(1, 0, 0, 44)
    P.BackgroundColor3 = Color3.fromRGB(14, 14, 22)
    P.BorderSizePixel = 0
    P.Parent = K
    Instance.new("UICorner", P).CornerRadius = UDim.new(0, 12)
    local Q = Instance.new("Frame")
    Q.Size = UDim2.new(1, 0, 0, 12)
    Q.Position = UDim2.new(0, 0, 1, -12)
    Q.BackgroundColor3 = Color3.fromRGB(14, 14, 22)
    Q.BorderSizePixel = 0
    Q.Parent = P
    local R = Instance.new("TextLabel")
    R.Font = Enum.Font.Michroma
    R.TextSize = 10
    R.TextColor3 = Color3.fromRGB(255, 255, 255)
    R.Size = UDim2.new(0, 120, 1, 0)
    R.Position = UDim2.new(0, 12, 0, 0)
    R.BackgroundTransparency = 1
    R.Text = L
    R.TextXAlignment = Enum.TextXAlignment.Left
    R.Parent = P
    local S = O and 140 or 108
    local T = Instance.new("TextButton")
    T.Size = UDim2.new(0, 30, 0, 22)
    T.Position = UDim2.new(1, -S, 0.5, -11)
    T.Text = "ES"
    T.Font = Enum.Font.GothamBold
    T.TextSize = 10
    T.Parent = P
    Instance.new("UICorner", T).CornerRadius = UDim.new(0, 5)
    local U = Instance.new("TextButton")
    U.Size = UDim2.new(0, 30, 0, 22)
    U.Position = UDim2.new(1, -(S-34), 0.5, -11)
    U.Text = "EN"
    U.Font = Enum.Font.GothamBold
    U.TextSize = 10
    U.Parent = P
    Instance.new("UICorner", U).CornerRadius = UDim.new(0, 5)
    A(T, not h) A(U, h)
    
    local W = Instance.new("TextButton")
    W.Size = UDim2.new(0, 26, 0, 26)
    W.Position = UDim2.new(1, -34, 0.5, -13)
    W.Text = "X"
    W.TextSize = 14
    W.Font = Enum.Font.GothamBold
    W.TextColor3 = Color3.fromRGB(255, 90, 110)
    W.BackgroundColor3 = Color3.fromRGB(28, 16, 22)
    W.Parent = P
    Instance.new("UICorner", W).CornerRadius = UDim.new(0, 6)
    W.MouseButton1Click:Connect(N)
    return P, T, U
end

local function X(Y, Z, aa, ab, ac, ad)
    local ae = Instance.new("TextButton")
    ae.Size = UDim2.new(1, -24, 0, 62)
    ae.Position = UDim2.new(0, 12, 0, Z)
    ae.BackgroundColor3 = Color3.fromRGB(16, 16, 26)
    ae.Text = ""
    ae.Parent = Y
    Instance.new("UICorner", ae).CornerRadius = UDim.new(0, 8)
    local af = Instance.new("UIStroke")
    af.Thickness = 1.2
    af.Color = Color3.fromRGB(32, 32, 48)
    af.Transparency = 0.4
    af.Parent = ae
    local ag = Instance.new("TextLabel")
    ag.Font = Enum.Font.GothamBold; ag.TextSize = 12; ag.TextColor3 = Color3.fromRGB(245, 245, 250)
    ag.Size = UDim2.new(1, -32, 0, 18); ag.Position = UDim2.new(0, 12, 0, 8); ag.BackgroundTransparency = 1
    ag.TextXAlignment = Enum.TextXAlignment.Left; ag.Text = aa; ag.Parent = ae
    local ah = Instance.new("TextLabel")
    ah.Font = Enum.Font.Ubuntu; ah.TextSize = 10; ah.TextColor3 = Color3.fromRGB(130, 140, 160)
    ah.Size = UDim2.new(1, -32, 0, 28); ah.Position = UDim2.new(0, 12, 0, 28); ah.BackgroundTransparency = 1
    ah.TextXAlignment = Enum.TextXAlignment.Left; ah.TextWrapped = true; ah.Text = ab; ah.Parent = ae
    local ai = Instance.new("TextLabel")
    ai.Font = Enum.Font.GothamBold; ai.TextSize = 13; ai.TextColor3 = Color3.fromRGB(60, 60, 80)
    ai.Size = UDim2.new(0, 16, 1, 0); ai.Position = UDim2.new(1, -20, 0, 0); ai.BackgroundTransparency = 1
    ai.Text = ">"; ai.Parent = ae
    ae.MouseEnter:Connect(function()
        c:Create(ae, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(22, 22, 38)}):Play()
        c:Create(af, TweenInfo.new(0.15), {Color = ac, Transparency = 0}):Play()
        c:Create(ag, TweenInfo.new(0.15), {TextColor3 = ac}):Play()
        c:Create(ai, TweenInfo.new(0.15), {TextColor3 = ac}):Play()
    end)
    ae.MouseLeave:Connect(function()
        c:Create(ae, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(16, 16, 26)}):Play()
        c:Create(af, TweenInfo.new(0.15), {Color = Color3.fromRGB(32, 32, 48), Transparency = 0.4}):Play()
        c:Create(ag, TweenInfo.new(0.15), {TextColor3 = Color3.fromRGB(245, 245, 250)}):Play()
        c:Create(ai, TweenInfo.new(0.15), {TextColor3 = Color3.fromRGB(60, 60, 80)}):Play()
    end)
    ae.MouseButton1Click:Connect(ad)
    return ag, ah
end

local function aj(ak, al)
    local am, an, ao
    ak.InputBegan:Connect(function(ap)
        if ap.UserInputType == Enum.UserInputType.MouseButton1 or ap.UserInputType == Enum.UserInputType.Touch then
            am = true an = ap.Position ao = al.Position
        end
    end)
    d.InputChanged:Connect(function(ap)
        if am and (ap.UserInputType == Enum.UserInputType.MouseMovement or ap.UserInputType == Enum.UserInputType.Touch) then
            local aq = ap.Position - an
            al.Position = UDim2.new(ao.X.Scale, ao.X.Offset + aq.X, ao.Y.Scale, ao.Y.Offset + aq.Y)
        end
    end)
    d.InputEnded:Connect(function(ap)
        if ap.UserInputType == Enum.UserInputType.MouseButton1 or ap.UserInputType == Enum.UserInputType.Touch then am = false end
    end)
end

local function ar(as, at, au, av)
    c:Create(at, TweenInfo.new(0.12), {Transparency = 1}):Play()
    local aw = c:Create(as, TweenInfo.new(0.18, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {Size = UDim2.new(0, au, 0, 0), Position = UDim2.new(0.5, -math.floor(au/2), 0.5, 0)})
    aw:Play()
    aw.Completed:Connect(function() as:Destroy() if av then av() end end)
end

do
    local aY, aZ = k(false), 270
    if j() then aY = k(true) aZ = 260 end
    local a_, aC2 = D(aY, aZ)
    a_.Name = "DeviceSelect"
    local b0, b1, b2 = J(a_, "HERMANOS CP", nil, function() z:Destroy() end, false)
    aj(b0, a_)
    local b3 = Instance.new("TextLabel")
    b3.Font = Enum.Font.Ubuntu; b3.TextSize = 11; b3.TextColor3 = Color3.fromRGB(150, 160, 185)
    b3.Size = UDim2.new(1, -24, 0, 18); b3.Position = UDim2.new(0, 12, 0, 50); b3.BackgroundTransparency = 1
    b3.TextXAlignment = Enum.TextXAlignment.Left; b3.Text = o().choose; b3.Parent = a_
    
    local b6, b7 = X(a_, 76, o().pc, o().pcD, Color3.fromRGB(0, 210, 255), function()
        ar(a_, aC2, aY, function() z:Destroy() s() end)
    end)
    local b8, b9 = X(a_, 146, o().mob, o().mobD, Color3.fromRGB(0, 255, 140), function()
        ar(a_, aC2, aY, function() z:Destroy() s() end)
    end)
    
    local function ba()
        local bb = o()
        b3.Text = bb.choose; b6.Text = bb.pc; b7.Text = bb.pcD; b8.Text = bb.mob; b9.Text = bb.mobD
        A(b1, not h); A(b2, h)
    end
    b1.MouseButton1Click:Connect(function() h = false ba() end)
    b2.MouseButton1Click:Connect(function() h = true ba() end)
end

print("[Hermanos CP] Unified Loaded | UID " .. e.UserId)
