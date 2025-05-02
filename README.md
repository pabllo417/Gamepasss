

```
local gamepasses = {
    -- IDs dos gamepasses que você deseja verificar
    123456789, -- Exemplo de ID de gamepass
}

local function hasGamepass(player, gamepassId)
    local hasPass = false
    local success, result = pcall(function()
        hasPass = game:GetService("MarketplaceService"):UserOwnsGamePassAsync(player.UserId, gamepassId)
    end)
    
    if success then
        return hasPass
    else
        warn("Erro ao verificar gamepass:", result)
        return false
    end
end

local function checkForAnyGamepass(player)
    for _, gamepassId in pairs(gamepasses) do
        if hasGamepass(player, gamepassId) then
            return true
        end
    end
    return false
end

game:GetService("Players").PlayerAdded:Connect(function(player)
    if checkForAnyGamepass(player) then
        -- Conceda acesso à funcionalidade específica aqui
        print(player.Name .. " possui um gamepass válido.")
        -- Exemplo: Dar um item ou habilidade especial
    else
        print(player.Name .. " não possui nenhum gamepass válido.")
    end
end)
```
