local TS, HS, Plrs = game:GetService("TeleportService"), game:GetService("HttpService"), game:GetService("Players")
local L, PID = Plrs.LocalPlayer, game.PlaceId

local function checkXbox()
    for _, p in ipairs(Plrs:GetPlayers()) do
        local ok, plat = pcall(function() return p.Platform end)
        if ok and (plat == Enum.Platform.XboxOne or plat == Enum.Platform.XBoxS) then
            return true
        end
    end
    return false
end

task.spawn(function()
    while task.wait(1.5) do
        if checkXbox() then
            break 
        else
            local ok, res = pcall(function()
                return HS:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/"..PID.."/servers/public?sortOrder=Desc&limit=100"))
            end)
            if ok and res and res.data then
                for _, s in ipairs(res.data) do
                    if s.playing >= 3 and s.playing < s.maxPlayers and s.id ~= game.JobId then
                        pcall(function()
                            TS:TeleportToPlaceInstance(PID, s.id, L)
                        end)
                        task.wait(3.5)
                        break
                    end
                end
            end
        end
    end
end)
