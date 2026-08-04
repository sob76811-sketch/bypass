--[========================================================================]--
-- Script: Xbox Console Server Finder & Smart Hopper for Delta
-- Game: BlockSpin (https://www.roblox.com/games/104715542330896/BlockSpin)
-- Description: Automatically hops between full servers until it detects 
--              a session populated predominantly by console/gamepad players.
--[========================================================================]--

local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local GuiService = game:GetService("GuiService")

local LocalPlayer = Players.LocalPlayer
local PlaceId = game.PlaceId

-- Configuration
local MIN_PLAYERS_PERCENTAGE = 0.85 -- 85% o mas de la sala debe ser de consola
local CHECK_DELAY = 4               -- Segundos de espera para que carguen los jugadores al entrar

-- Notificación visual rápida en Delta
local function notify(text)
    pcall(function()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Xbox Server Finder",
            Text = text,
            Duration = 3
        })
    end)
end

-- Función para evaluar si el servidor actual es de consola/mando
local function isConsoleServer()
    local totalPlayers = #Players:GetPlayers()
    if totalPlayers <= 1 then return false end
    
    local consoleCount = 0
    
    for _, player in ipairs(Players:GetPlayers()) do
        -- Detección por plataforma o si usa mando/interfaz de consola
        local success, platform = pcall(function()
            return player.Platform
        end)
        
        -- Si la API detecta consola o si el tipo de dispositivo/input apunta a Xbox/Console
        if success and (platform == Enum.Platform.XboxOne or platform == Enum.Platform.XBoxS or platform == Enum.Platform.PS4 or platform == Enum.Platform.PS5) then
            consoleCount = consoleCount + 1
        else
            -- Verificación alternativa por atributos comunes o sesiones cruzadas
            local hasAttribute, isConsoleAttr = pcall(function()
                return player:GetAttribute("IsConsole") or player:GetAttribute("Platform")
            end)
            if hasAttribute and (isConsoleAttr == "Xbox" or isConsoleAttr == true) then
                consoleCount = consoleCount + 1
            end
        end
    end
    
    local ratio = consoleCount / totalPlayers
    return ratio >= MIN_PLAYERS_PERCENTAGE
end

-- Función para buscar y saltar a servidores llenos
local function forceConsoleHop()
    notify("Buscando otro servidor lleno de consola...")
    
    local success, response = pcall(function()
        local url = string.format("https://games.roblox.com/v1/games/%d/servers/public?sortOrder=Desc&limit=100", PlaceId)
        return HttpService:JSONDecode(game:HttpGet(url))
    end)
    
    if success and response and response.data then
        for _, server in ipairs(response.data) do
            -- Filtra servidores llenos (ej. que queden menos de 4 espacios libres) y que no sea el actual
            if server.playing >= (server.maxPlayers - 4) and server.id ~= game.JobId then
                pcall(function()
                    TeleportService:TeleportToPlaceInstance(PlaceId, server.id, LocalPlayer)
                end)
                task.wait(8) -- Espera prudente para evitar bucles de teletransporte fallidos
                break
            end
        end
    else
        notify("Error al conectar con la API. Reintentando...")
        task.wait(3)
    end
end

-- Ciclo principal del buscador
notify("Iniciando buscador de servidores Xbox...")

task.spawn(function()
    while true do
        task.wait(CHECK_DELAY)
        
        if isConsoleServer() then
            notify("¡Servidor exclusivo de consola encontrado y lleno!")
            print("[Xbox Finder]: ¡Listo! Te has quedado en un servidor de consola.")
            break -- Detiene el script porque ya encontró la sala ideal
        else
            forceConsoleHop()
        end
    end
end)
