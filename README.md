local TS, HS, Plrs = game:GetService("TeleportService"), game:GetService("HttpService"), game:GetService("Players")
local L, PID = Plrs.LocalPlayer, game.PlaceId

task.spawn(function()
    while task.wait(0.5) do
        local ok, res = pcall(function()
            return HS:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/"..PID.."/servers/public?sortOrder=Asc&limit=100"))
        end)
        
        if ok and res and res.data then
            for _, s in ipairs(res.data) do
                if s.playing <= 20 and s.playing > 1 and s.id ~= game.JobId then
                    pcall(function()
                        TS:TeleportToPlaceInstance(PID, s.id, L)
                    end)
                    break
                end
            end
        end
    end
end)
