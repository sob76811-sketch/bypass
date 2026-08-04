local TS, HS, Plrs = game:GetService("TeleportService"), game:GetService("HttpService"), game:GetService("Players")
local L, PID = Plrs.LocalPlayer, game.PlaceId

local function hasXboxPlayer()
    for _, gui in ipairs(CoreGui:GetDescendants()) do
        -- Detecta si en la lista de jugadores actual hay elementos de Xbox
        if gui:IsA("ImageLabel") and string.find(gui.Image, "xbox") then
            return true
        end
    end
    -- Verificación alterna por plataforma del cliente interno si está disponible
    for _, p in ipairs(Plrs:GetPlayers()) do
        local success, plat = pcall(function() return p.Platform end)
        if success and (plat == Enum.Platform.XboxOne or plat == Enum.Platform.XBoxS) then
            return true
        end
    end
    return false
end

task.spawn(function()
    while task.wait(1) do
        if hasXboxPlayer() then
            print("[Xbox Finder]: ¡Servidor con gente de Xbox encontrado!")
            break -- Se detiene y se queda en este servidor
        else
            local ok, res = pcall(function()
                return HS:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/"..PID.."/servers/public?sortOrder=Asc&limit=100"))
            end)
            
            if ok and res and res.data then
                for _, s in ipairs(res.data) do
                    if s.playing <= 20 and s.playing > 0 and s.id ~= game.JobId then
                        pcall(function()
                            TS:TeleportToPlaceInstance(PID, s.id, L)
                        end)
                        task.wait(4)
                        break
                    end
                end
            end
        end
    end
end)
