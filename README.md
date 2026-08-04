--[==[ Delta Optimized Xbox/Console Server Finder ]==]--
local TS, HS, Plrs = game:GetService("TeleportService"), game:GetService("HttpService"), game:GetService("Players")
local L, PID = Plrs.LocalPlayer, game.PlaceId

task.spawn(function()
    while task.wait(2.5) do
        local ok, res = pcall(function()
            return HS:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/"..PID.."/servers/public?sortOrder=Asc&limit=100"))
        end)
        
        if ok and res and res.data then
            for _, s in ipairs(res.data) do
                -- Busca servidores con 20 jugadores o menos (mayor probabilidad de salas de consola/amigos) pero que no estén vacíos
                if s.playing <= 20 and s.playing > 1 and s.id ~= game.JobId then
                    pcall(function()
                        TS:TeleportToPlaceInstance(PID, s.id, L)
                    end)
                    task.wait(5)
                    break
                end
            end
        end
    end
end)
