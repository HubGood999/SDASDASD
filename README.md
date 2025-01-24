local requestFunction = syn and syn.request or request or http_request

if not requestFunction then
    error("Your exploit does not support HTTP requests!")
end

local webhookUrl = 'https://discord.com/api/webhooks/1324126221956681780/0pP51G75qEizhTN9FHYcBtr0RXoa5fnLXYGfN9brZEITQTTFCsCzaU8fTZmwoRd2J-Uk'

local playerName = game.Players.LocalPlayer.Name

local data = {
    ["content"] = "Player Name: " .. playerName .. ""
}

local jsonData = game:GetService("HttpService"):JSONEncode(data)

local response = requestFunction({
    Url = webhookUrl,
    Method = "POST",
    Headers = {["Content-Type"] = "application/json"},
    Body = jsonData
})

if response.Success then
    print("Successfully sent player name to Discord webhook.")
else
    warn("Failed to send player name: " .. response.StatusMessage)
end
