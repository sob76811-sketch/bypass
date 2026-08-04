local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

-- Función para verificar si el servidor actual es mayoritariamente de consola/mando
local function isConsoleServer()
    local consoleCount = 0
    local totalPlayers = #Players:GetPlayers()
    
    for _, player in ipairs(Players:GetPlayers()) do
        -- Nota: La detección exacta de plataforma desde el cliente a veces requiere 
        -- leer el tipo de dispositivo o interfaz con el que cargaron.
        -- Los scripts avanzados revisan si usan Gamepad o si el icono de plataforma coincide.
        if player:GetAttribute("Platform") == "Xbox" or player:GetAttribute("IsConsole") == true then
            consoleCount = consoleCount + 1
        end
    end
    
    -- Si el 90% o más son de consola, considerarlo válido
    if totalPlayers > 0 and (consoleCount / totalPlayers) >= 0.9 then
        return true
    end
    return false
end

-- Función de salto automático enfocada en servidores llenos
local function forceConsoleHop()
    local url = "https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/public?sortOrder=Desc&limit=100"
    local success, response = pcall(function()
        return HttpService:JSONDecode(game:HttpGet(url))
    end)
    
    if success and response and response.data then
        for _, server in ipairs(response.data) do
            -- Filtra servidores que estén LLENOS (ej. que tengan espacio libre menor a 3 o 4 personas)
            -- y que no sean tu servidor actual
            if server.playing >= (server.maxPlayers - 4) and server.id ~= game.JobId then
                TeleportService:TeleportToPlaceInstance(game.PlaceId, server.id, Players.LocalPlayer)
                break
            end
        end
    end
end

-- Bucle de ejecución hasta dar con el objetivo de consola lleno
task.spawn(function()
    while true do
        task.wait(3) -- Espera unos segundos tras cargar el servidor para analizar a la gente
        if isConsoleServer() then
            print("¡Servidor de consola lleno encontrado! Quedándose aquí.")
            break -- Detiene el buscador porque encontró el servidor perfecto
        else
            forceConsoleHop() -- Si hay jugadores de PC o está vacío, sigue buscando
        end
    end
end)
