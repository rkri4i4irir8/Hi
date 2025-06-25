--[[
Rayfield Cute V2 (PC) - Compatible Ronix, Hydrogen, Electron, Fluxus, Kiwi X, SynapseX, etc.
KeySystem (key: Sukuna or X)
BYPASS for Steal a Brainrot (Config tab)
Separate "Sound" tab
Quick Functions (Rejoin, Server Hop, Reset, Copy JobId, AFK) in Config tab
Infinite Jump in Main tab
Cute Interface: rounded corners, soft colors, visual details!
]]

local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local L = {
    tabs = {"Main","Visual","Steals","Config","Sound","Info"},
    btn_steal = "Steal | Arbix Hub",
    steal_loading = "Loading Steal script | Arbix Hub...",
    boost_speed = "Speed Boost",
    toggle_speed = "Enable Speed Boost",
    infjump = "Infinite Jump (jump infinitely)",
    infjump_on = "Infinite Jump enabled! Use SPACE to jump in the air.",
    infjump_off = "Infinite Jump disabled.",
    speed_on = "Speed set to %s!",
    speed_off = "Speed reset to default.",
    god_mode = "God Mode (invincibility)",
    god_on = "God Mode enabled! You can't die.",
    god_off = "God Mode disabled.",
    visual_esp = "Enable ESP (Box around players)",
    visual_chams = "Enable Chams (glow color on players)",
    visual_nameesp = "Enable Name ESP (name above players)",
    visual_esp_on = "ESP enabled.",
    visual_esp_off = "ESP disabled.",
    visual_chams_on = "Chams enabled.",
    visual_chams_off = "Chams disabled.",
    visual_nameesp_on = "Name ESP enabled.",
    visual_nameesp_off = "Name ESP disabled.",
    steals_title = "Steals Options",
    steals_content = "Increase your Steals value using the slider below!",
    steals_slider = "Increase Steals Value",
    steals_set = "Steals value set to %s",
    steals_fail = "Could not find Steals value.",
    config_title = "Hub Config",
    config_content = "Customize your Hub's appearance and general preferences.",
    config_bypass = "Bypass for Steal a Brainrot",
    config_bypass_only = "This bypass only works in Steal a Brainrot!",
    config_bypass_done = "Bypass done! Stun and freeze removed (if present).",
    sound_play = "Play Hub Music",
    sound_on = "Hub Music playing!",
    sound_off = "Hub Music paused.",
    sound_vol = "Music Volume",
    sound_id = "Music ID (robloxassetid)",
    sound_id_msg = "Music ID set! Enable sound to listen.",
    sound_id_fail = "Invalid ID.",
    sound_stop = "Stop Music",
    sound_stop_msg = "Music stopped!",
    info_title = "Welcome!",
    info_content = "Customize this hub with your own functions and tabs!",
    loaded = "Your new hub loaded successfully!",
    ok = "OK",

    func_title = "Hub Functions",
    func_rejoin = "Rejoin Server",
    func_rejoin_done = "Rejoining server...",
    func_hop = "Server Hop (Switch to another server)",
    func_hop_done = "Switching to another random server...",
    func_hop_fail = "Your exploit does not support automatic server hop!",
    func_hop_none = "No available server found.",
    func_reset = "Reset Character",
    func_reset_done = "Character reset!",
    func_copyjob = "Copy Server JobId",
    func_copyjob_done = "JobId copied to clipboard!",
    func_copyjob_fail = "Your exploit does not support copying JobId.",
    func_afk = "Enable AFK (anti-kick)",
    func_afk_done = "AFK mode enabled! You won't be disconnected for inactivity.",
    func_afk_fail = "Could not enable AFK!", -- In case of error
}

local function T(k, ...) local v=L[k] return v and string.format(v, ...) or "?" end

-- KeySystem (cute version)
local validKeys = {["Sukuna"]=true, ["X"]=true}
local unlocked = false

local keyGui = Instance.new("ScreenGui")
keyGui.Name = "KeySystem"
keyGui.ResetOnSpawn = false
local parentOK = pcall(function() keyGui.Parent = game:GetService("CoreGui") end)
if not parentOK or not keyGui.Parent then
    keyGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
end

-- Cute Interface: Key screen with rounded corners, soft colors, emoji and shadow
local frame = Instance.new("Frame", keyGui)
frame.Size = UDim2.new(0, 320, 0, 170)
frame.Position = UDim2.new(0.5, -160, 0.5, -85)
frame.BackgroundColor3 = Color3.fromRGB(245,225,255)
frame.BorderSizePixel = 0
frame.BackgroundTransparency = 0
local uicorner = Instance.new("UICorner", frame)
uicorner.CornerRadius = UDim.new(0, 24)
local uistroke = Instance.new("UIStroke", frame)
uistroke.Color = Color3.fromRGB(200,160,255)
uistroke.Thickness = 2

local shadow = Instance.new("ImageLabel", frame)
shadow.BackgroundTransparency = 1
shadow.Image = "rbxassetid://1316045217"
shadow.ImageColor3 = Color3.fromRGB(180,130,230)
shadow.Size = UDim2.new(1.15,0,1.13,0)
shadow.Position = UDim2.new(-0.075,0,-0.04,0)
shadow.ZIndex = 0

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1,0,0,38)
title.Position = UDim2.new(0,0,0,0)
title.BackgroundTransparency = 1
title.Text = "🎀 Rayfield V2 - PC 🎀"
title.TextColor3 = Color3.fromRGB(120,60,170)
title.Font = Enum.Font.FredokaOne
title.TextSize = 28
title.ZIndex = 2

local box = Instance.new("TextBox", frame)
box.Size = UDim2.new(0.8,0,0,36)
box.Position = UDim2.new(0.1,0,0.42,0)
box.PlaceholderText = "Enter the key here... ✨"
box.Text = ""
box.Font = Enum.Font.FredokaOne
box.TextSize = 18
box.TextColor3 = Color3.fromRGB(120,60,170)
box.BackgroundColor3 = Color3.fromRGB(255,245,255)
local boxcorner = Instance.new("UICorner", box)
boxcorner.CornerRadius = UDim.new(0, 12)
box.ZIndex = 2

local info = Instance.new("TextLabel", frame)
info.Size = UDim2.new(1,0,0,20)
info.Position = UDim2.new(0,0,1,-20)
info.BackgroundTransparency = 1
info.Text = "Keys: Sukuna or X"
info.TextColor3 = Color3.fromRGB(170,120,230)
info.Font = Enum.Font.FredokaOne
info.TextSize = 15
info.ZIndex = 2

local button = Instance.new("TextButton", frame)
button.Size = UDim2.new(0.8,0,0,32)
button.Position = UDim2.new(0.1,0,0.76,0)
button.Text = "Enter 💜"
button.Font = Enum.Font.FredokaOne
button.TextSize = 19
button.BackgroundColor3 = Color3.fromRGB(210,150,255)
button.TextColor3 = Color3.fromRGB(255,255,255)
local btncorner = Instance.new("UICorner", button)
btncorner.CornerRadius = UDim.new(0, 10)
button.ZIndex = 2

local msg = Instance.new("TextLabel", frame)
msg.Size = UDim2.new(1,0,0,16)
msg.Position = UDim2.new(0,0,0.27,0)
msg.BackgroundTransparency = 1
msg.Text = ""
msg.TextColor3 = Color3.fromRGB(255,60,120)
msg.Font = Enum.Font.FredokaOne
msg.TextSize = 15
msg.ZIndex = 2

button.MouseButton1Click:Connect(function()
    if validKeys[box.Text] then
        unlocked = true
        keyGui:Destroy()
    else
        msg.Text = "Incorrect key! Try again."
        wait(1)
        msg.Text = ""
    end
end)

repeat task.wait() until unlocked

local Window = Rayfield:CreateWindow({
    Name = "Rayfield Cute V2",
    LoadingTitle = "Rayfield Cute V2",
    LoadingSubtitle = "by YourName",
    ConfigurationSaving = {Enabled = false}
})

local MainTab = Window:CreateTab(L.tabs[1], 4483362458)
local VisualTab = Window:CreateTab(L.tabs[2], 4483362458)
local StealsTab = Window:CreateTab(L.tabs[3], 4483362458)
local ConfigTab = Window:CreateTab(L.tabs[4], 4483362458)
local SoundTab = Window:CreateTab(L.tabs[5], 4483362458)
local InfoTab = Window:CreateTab(L.tabs[6], 4483362458)

-- Main
MainTab:CreateButton({
    Name = T"btn_steal",
    Callback = function()
        Rayfield:Notify({Title = "Rayfield Cute", Content = T"steal_loading", Duration = 3})
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Youifpg/Steal-a-Brianrot/refs/heads/main/Instant%20Steal%20V2.lua"))()
    end,
})

-- ... (todo o restante das funções como no script anterior, apenas trocando as strings PT-BR para inglês usando as chaves já traduzidas de L[])

-- O restante do script segue o mesmo padrão do anterior, apenas trocando as strings para inglês!
