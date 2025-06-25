--[[
Novo Hub Rayfield V2 (PC) - Compatível Ronix, Hydrogen, Electron, Fluxus, Kiwi X, SynapseX, etc.
KeySystem funcional (key: Sukuna ou X)
BYPASS para Steal a Brainrot (aba Configuração)
Aba "Som" separada
Funções rápidas (Rejoin, Server Hop, Reset, Copiar JobId) na aba Configuração
Infinite Jump na aba Principal
Interface Fofinho: cantos arredondados, cores suaves e detalhes visuais!
]]

local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local L = {
    tabs = {"Principal","Visual","Steals","Configuração","Som","Info"},
    btn_steal = "Steal | Arbix Hub",
    steal_loading = "Carregando script Steal | Arbix Hub...",
    boost_speed = "Boost de Velocidade",
    toggle_speed = "Ativar Boost de Velocidade",
    infjump = "Infinite Jump (pular infinitamente)",
    infjump_on = "Infinite Jump ativado! Use ESPAÇO para pular no ar.",
    infjump_off = "Infinite Jump desativado.",
    speed_on = "Velocidade aumentada para %s!",
    speed_off = "Velocidade resetada para padrão.",
    god_mode = "God Mode (imortalidade)",
    god_on = "God Mode ativado! Você não pode morrer.",
    god_off = "God Mode desativado.",
    visual_esp = "Ativar ESP (Box ao redor dos players)",
    visual_chams = "Ativar Chams (cor brilhante nos players)",
    visual_nameesp = "Ativar Name ESP (nome acima dos players)",
    visual_esp_on = "ESP ativado.",
    visual_esp_off = "ESP desativado.",
    visual_chams_on = "Chams ativado.",
    visual_chams_off = "Chams desativado.",
    visual_nameesp_on = "Name ESP ativado.",
    visual_nameesp_off = "Name ESP desativado.",
    steals_title = "Opções de Steals",
    steals_content = "Aumente o valor de Steals usando o slider abaixo!",
    steals_slider = "Aumentar Valor de Steals",
    steals_set = "Valor de Steals definido para %s",
    steals_fail = "Não foi possível encontrar o valor de Steals.",
    config_title = "Configuração do Hub",
    config_content = "Personalize o visual do seu Hub e preferências gerais.",
    config_bypass = "Bypass para Steal a Brainrot",
    config_bypass_only = "Esse bypass só funciona no Steal a Brainrot!",
    config_bypass_done = "Bypass executado! Stun e freeze removidos (se existirem).",
    sound_play = "Tocar Música do Hub",
    sound_on = "Música do Hub tocando!",
    sound_off = "Música do Hub pausada.",
    sound_vol = "Volume da Música",
    sound_id = "ID da Música (robloxassetid)",
    sound_id_msg = "ID da música definida! Ative o som para ouvir.",
    sound_id_fail = "ID inválido.",
    sound_stop = "Parar Música",
    sound_stop_msg = "Música parada!",
    info_title = "Bem-vindo!",
    info_content = "Personalize este hub com suas próprias funções e abas!",
    loaded = "Seu novo hub foi carregado com sucesso!",
    ok = "OK",

    func_title = "Funções do Hub",
    func_rejoin = "Reentrar no servidor",
    func_rejoin_done = "Reentrando no servidor...",
    func_hop = "Server Hop (Trocar de servidor)",
    func_hop_done = "Trocando para outro servidor aleatório...",
    func_hop_fail = "Seu exploit não suporta server hop automático!",
    func_hop_none = "Nenhum servidor disponível encontrado.",
    func_reset = "Resetar Personagem",
    func_reset_done = "Personagem resetado!",
    func_copyjob = "Copiar JobId do servidor",
    func_copyjob_done = "JobId copiado para área de transferência!",
    func_copyjob_fail = "Seu exploit não suporta copiar JobId.",
}

local function T(k, ...) local v=L[k] return v and string.format(v, ...) or "?" end

-- KeySystem simples (função fofinha)
local validKeys = {["Sukuna"]=true, ["X"]=true}
local unlocked = false

local keyGui = Instance.new("ScreenGui")
keyGui.Name = "KeySystem"
keyGui.ResetOnSpawn = false
local parentOK = pcall(function() keyGui.Parent = game:GetService("CoreGui") end)
if not parentOK or not keyGui.Parent then
    keyGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
end

-- Interface Fofinho: Tela de key com cantos arredondados, cores suaves, emoji e sombra
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
box.PlaceholderText = "Digite a key aqui... ✨"
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
info.Text = "Keys: Sukuna ou X"
info.TextColor3 = Color3.fromRGB(170,120,230)
info.Font = Enum.Font.FredokaOne
info.TextSize = 15
info.ZIndex = 2

local button = Instance.new("TextButton", frame)
button.Size = UDim2.new(0.8,0,0,32)
button.Position = UDim2.new(0.1,0,0.76,0)
button.Text = "Entrar 💜"
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
        msg.Text = "Key incorreta! Tente novamente."
        wait(1)
        msg.Text = ""
    end
end)

repeat task.wait() until unlocked

local Window = Rayfield:CreateWindow({
    Name = "Rayfield Fofinho V2",
    LoadingTitle = "Rayfield Fofinho V2",
    LoadingSubtitle = "by SeuNome",
    ConfigurationSaving = {Enabled = false}
})

local MainTab = Window:CreateTab(L.tabs[1], 4483362458)
local VisualTab = Window:CreateTab(L.tabs[2], 4483362458)
local StealsTab = Window:CreateTab(L.tabs[3], 4483362458)
local ConfigTab = Window:CreateTab(L.tabs[4], 4483362458)
local SoundTab = Window:CreateTab(L.tabs[5], 4483362458)
local InfoTab = Window:CreateTab(L.tabs[6], 4483362458)

-- Principal
MainTab:CreateButton({
    Name = T"btn_steal",
    Callback = function()
        Rayfield:Notify({Title = "Rayfield Fofinho", Content = T"steal_loading", Duration = 3})
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Youifpg/Steal-a-Brianrot/refs/heads/main/Instant%20Steal%20V2.lua"))()
    end,
})

local speedValue = 16
local speedActive = false
local speedConn = nil

MainTab:CreateSlider({
    Name = T"boost_speed",
    Range = {16, 200},
    Increment = 1,
    Suffix = "Speed",
    CurrentValue = 16,
    Callback = function(value)
        speedValue = value
        if speedActive and game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
            game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = speedValue
        end
    end,
})

MainTab:CreateToggle({
    Name = T"toggle_speed",
    CurrentValue = false,
    Callback = function(state)
        speedActive = state
        local player = game.Players.LocalPlayer
        if speedActive then
            if player and player.Character and player.Character:FindFirstChildOfClass("Humanoid") then
                player.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = speedValue
            end
            if speedConn then speedConn:Disconnect() end
            speedConn = player.CharacterAdded:Connect(function(char)
                local hum = char:WaitForChild("Humanoid", 5)
                if hum and speedActive then
                    hum.WalkSpeed = speedValue
                end
            end)
            Rayfield:Notify({
                Title = T"boost_speed",
                Content = T("speed_on", tostring(speedValue)),
                Duration = 3,
            })
        else
            if player and player.Character and player.Character:FindFirstChildOfClass("Humanoid") then
                player.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = 16
            end
            if speedConn then speedConn:Disconnect() end
            Rayfield:Notify({
                Title = T"boost_speed",
                Content = T"speed_off",
                Duration = 3,
            })
        end
    end,
})

-- Infinite Jump FOFINHO
local infjumpActive = false
local infjumpConn = nil
MainTab:CreateToggle({
    Name = T"infjump",
    CurrentValue = false,
    Callback = function(state)
        infjumpActive = state
        if infjumpConn then infjumpConn:Disconnect() infjumpConn = nil end
        if infjumpActive then
            infjumpConn = game:GetService("UserInputService").JumpRequest:Connect(function()
                local plr = game.Players.LocalPlayer
                if plr and plr.Character and plr.Character:FindFirstChildOfClass("Humanoid") then
                    local hum = plr.Character:FindFirstChildOfClass("Humanoid")
                    if hum and hum:GetState() ~= Enum.HumanoidStateType.Dead then
                        hum:ChangeState(Enum.HumanoidStateType.Jumping)
                    end
                end
            end)
            Rayfield:Notify({Title=T"infjump", Content=T"infjump_on", Duration=3})
        else
            Rayfield:Notify({Title=T"infjump", Content=T"infjump_off", Duration=3})
        end
    end,
})

local godActive = false
local godConn = nil

MainTab:CreateToggle({
    Name = T"god_mode",
    CurrentValue = false,
    Callback = function(state)
        godActive = state
        local player = game.Players.LocalPlayer
        local function enableGod()
            if player and player.Character and player.Character:FindFirstChildOfClass("Humanoid") then
                local hum = player.Character:FindFirstChildOfClass("Humanoid")
                hum.Health = hum.MaxHealth
                hum:GetPropertyChangedSignal("Health"):Connect(function()
                    if godActive and hum.Health < hum.MaxHealth then
                        hum.Health = hum.MaxHealth
                    end
                end)
                if hum:FindFirstChild("creator") then
                    hum.creator:Destroy()
                end
            end
        end
        if godActive then
            enableGod()
            if godConn then godConn:Disconnect() end
            godConn = player.CharacterAdded:Connect(function()
                wait(0.2)
                enableGod()
            end)
            Rayfield:Notify({
                Title = T"god_mode",
                Content = T"god_on",
                Duration = 3,
            })
        else
            if godConn then godConn:Disconnect() end
            Rayfield:Notify({
                Title = T"god_mode",
                Content = T"god_off",
                Duration = 3,
            })
        end
    end,
})

-- Visual
VisualTab:CreateToggle({
    Name = T"visual_esp",
    CurrentValue = false,
    Callback = function(state)
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character then
                if state then
                    if not player.Character:FindFirstChild("ESPBox") then
                        local box = Instance.new("BoxHandleAdornment", player.Character)
                        box.Name = "ESPBox"
                        box.Adornee = player.Character:FindFirstChild("HumanoidRootPart") or player.Character:FindFirstChildWhichIsA("BasePart")
                        box.AlwaysOnTop = true
                        box.ZIndex = 10
                        box.Size = Vector3.new(4,6,2)
                        box.Color3 = Color3.fromRGB(255,120,220)
                        box.Transparency = 0.6
                    end
                else
                    if player.Character:FindFirstChild("ESPBox") then
                        player.Character.ESPBox:Destroy()
                    end
                end
            end
        end
        Rayfield:Notify({
            Title = T"tabs",
            Content = state and T"visual_esp_on" or T"visual_esp_off",
            Duration = 3,
        })
    end,
})
VisualTab:CreateToggle({
    Name = T"visual_chams",
    CurrentValue = false,
    Callback = function(state)
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character then
                for _, part in pairs(player.Character:GetChildren()) do
                    if part:IsA("BasePart") then
                        if state then
                            part.Color = Color3.fromRGB(190,110,255)
                            part.Material = Enum.Material.Neon
                        else
                            part.Color = Color3.new(1,1,1)
                            part.Material = Enum.Material.Plastic
                        end
                    end
                end
            end
        end
        Rayfield:Notify({
            Title = T"tabs",
            Content = state and T"visual_chams_on" or T"visual_chams_off",
            Duration = 3,
        })
    end,
})
VisualTab:CreateToggle({
    Name = T"visual_nameesp",
    CurrentValue = false,
    Callback = function(state)
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character then
                if state then
                    if not player.Character:FindFirstChild("NameBillboard") then
                        local billboard = Instance.new("BillboardGui", player.Character)
                        billboard.Name = "NameBillboard"
                        billboard.Adornee = player.Character:FindFirstChild("Head")
                        billboard.Size = UDim2.new(0,100,0,40)
                        billboard.AlwaysOnTop = true

                        local text = Instance.new("TextLabel", billboard)
                        text.Size = UDim2.new(1,0,1,0)
                        text.BackgroundTransparency = 1
                        text.Text = "🌸 "..player.Name.." 🌸"
                        text.TextColor3 = Color3.fromRGB(220,120,255)
                        text.TextStrokeTransparency = 0.25
                        text.Font = Enum.Font.FredokaOne
                        text.TextScaled = true
                    end
                else
                    if player.Character:FindFirstChild("NameBillboard") then
                        player.Character.NameBillboard:Destroy()
                    end
                end
            end
        end
        Rayfield:Notify({
            Title = T"tabs",
            Content = state and T"visual_nameesp_on" or T"visual_nameesp_off",
            Duration = 3,
        })
    end,
})

-- Steals
StealsTab:CreateParagraph({Title = T"steals_title", Content = T"steals_content"})
StealsTab:CreateSlider({
    Name = T"steals_slider",
    Range = {0, 100000},
    Increment = 1,
    Suffix = "Steals",
    CurrentValue = 0,
    Callback = function(value)
        local p = game:GetService("Players").LocalPlayer
        local steals = p:FindFirstChild("leaderstats") and p.leaderstats:FindFirstChild("Steals")
        if steals and typeof(steals.Value) == "number" then
            steals.Value = value
            Rayfield:Notify({
                Title = T"steals_title",
                Content = T("steals_set", tostring(steals.Value)),
                Duration = 3,
            })
        else
            Rayfield:Notify({
                Title = T"steals_title",
                Content = T"steals_fail",
                Duration = 3,
            })
        end
    end,
})

-- Configuração (Funções)
ConfigTab:CreateParagraph({Title = T"config_title", Content = T"config_content"})
ConfigTab:CreateParagraph({Title = T"func_title", Content = ""})

ConfigTab:CreateButton({
    Name = T"func_rejoin",
    Callback = function()
        Rayfield:Notify({Title=T"func_rejoin",Content=T"func_rejoin_done",Duration=3})
        game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId, game.JobId, game.Players.LocalPlayer)
    end,
})

ConfigTab:CreateButton({
    Name = T"func_hop",
    Callback = function()
        local httpok, HttpService = pcall(game.GetService, game, "HttpService")
        local telok, TeleportService = pcall(game.GetService, game, "TeleportService")
        Rayfield:Notify({Title=T"func_hop",Content=T"func_hop_done",Duration=3})
        local PlaceId = game.PlaceId
        local Servers = {}
        local req = (syn and syn.request) or (fluxus and fluxus.request) or http and http.request or http_request or request
        if not req then
            Rayfield:Notify({Title="Server Hop",Content=T"func_hop_fail",Duration=4}) return
        end
        if not (httpok and telok) then
            Rayfield:Notify({Title="Server Hop",Content=T"func_hop_fail",Duration=4}) return
        end
        local success, response = pcall(req, {Url = "https://games.roblox.com/v1/games/"..PlaceId.."/servers/Public?sortOrder=Desc&limit=100"})
        if not success then
            Rayfield:Notify({Title="Server Hop",Content=T"func_hop_fail",Duration=4}) return
        end
        local body = HttpService:JSONDecode(response.Body)
        for i,v in pairs(body.data) do
            if v.playing < v.maxPlayers and v.id ~= game.JobId then
                table.insert(Servers,v.id)
            end
        end
        if #Servers > 0 then
            TeleportService:TeleportToPlaceInstance(PlaceId, Servers[math.random(1,#Servers)], game.Players.LocalPlayer)
        else
            Rayfield:Notify({Title="Server Hop",Content=T"func_hop_none",Duration=4})
        end
    end,
})

ConfigTab:CreateButton({
    Name = T"func_reset",
    Callback = function()
        local player = game.Players.LocalPlayer
        if player and player.Character and player.Character:FindFirstChildOfClass("Humanoid") then
            player.Character:FindFirstChildOfClass("Humanoid").Health = 0
            Rayfield:Notify({Title=T"func_reset",Content=T"func_reset_done",Duration=3})
        end
    end,
})

ConfigTab:CreateButton({
    Name = T"func_copyjob",
    Callback = function()
        local setclip = setclipboard or toclipboard or (syn and syn.write_clipboard)
        if setclip then
            setclip(game.JobId)
            Rayfield:Notify({Title=T"func_copyjob",Content=T"func_copyjob_done",Duration=3})
        else
            Rayfield:Notify({Title=T"func_copyjob",Content=T"func_copyjob_fail",Duration=3})
        end
    end,
})

ConfigTab:CreateButton({
    Name = T"config_bypass",
    Callback = function()
        if game.PlaceId ~= 109983668079237 then
            Rayfield:Notify({Title=T"config_bypass",Content=T"config_bypass_only",Duration=3}); return
        end
        local char = game.Players.LocalPlayer.Character
        if char then
            if char:FindFirstChild("Stunned") then char.Stunned:Destroy() end
            if char:FindFirstChild("Freeze") then char.Freeze:Destroy() end
        end
        Rayfield:Notify({Title=T"config_bypass",Content=T"config_bypass_done",Duration=3})
    end,
})

-- SOM
local sound = game:GetService("Players").LocalPlayer:FindFirstChild("HubSound")
if not sound then
    sound = Instance.new("Sound")
    sound.Name = "HubSound"
    sound.Parent = game:GetService("Players").LocalPlayer
    sound.SoundId = "rbxassetid://1843526937"
    sound.Volume = 1
    sound.Looped = true
end
SoundTab:CreateToggle({
    Name = T"sound_play",
    CurrentValue = false,
    Callback = function(state)
        if state then
            sound:Play()
            Rayfield:Notify({Title=T"sound_play",Content=T"sound_on",Duration=3})
        else
            sound:Pause()
            Rayfield:Notify({Title=T"sound_play",Content=T"sound_off",Duration=3})
        end
    end,
})
SoundTab:CreateSlider({
    Name = T"sound_vol",
    Range = {0, 5},
    Increment = 0.05,
    Suffix = "",
    CurrentValue = sound.Volume,
    Callback = function(value)
        sound.Volume = value
        Rayfield:Notify({Title=T"sound_vol",Content=T("sound_vol", math.floor(value*100)),Duration=2})
    end,
})
SoundTab:CreateInput({
    Name = T"sound_id",
    PlaceholderText = "Ex: 1843526937",
    RemoveTextAfterFocusLost = true,
    Callback = function(text)
        text = text:gsub("[^%d]", "")
        if #text > 0 then
            sound.SoundId = "rbxassetid://"..text
            Rayfield:Notify({Title=T"sound_id",Content=T"sound_id_msg",Duration=3})
        else
            Rayfield:Notify({Title=T"sound_id",Content=T"sound_id_fail",Duration=3})
        end
    end,
})
SoundTab:CreateButton({
    Name = T"sound_stop",
    Callback = function()
        sound:Stop()
        Rayfield:Notify({Title=T"sound_stop",Content=T"sound_stop_msg",Duration=3})
    end,
})

-- Info
InfoTab:CreateParagraph({Title = T"info_title", Content = T"info_content"})
Rayfield:Notify({Title = "Rayfield Fofinho", Content = T"loaded", Duration = 4, Actions = {{Name = T"ok", Callback = function() end}}})
