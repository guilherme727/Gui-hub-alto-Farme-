# Gui-hub-alto-Farme-

*Gui Hub Farm Bot*

```
-- Configurações
getgenv().nomeScript = "Gui Hub Farm Bot"
getgenv().fruitParaFarmar = "Light Fruit"
getgenv().tempoDeAtaque = 0.1
getgenv().distanciaDeAtaque = 15
getgenv().levelMinimo = 100
getgenv().paused = false

-- Farm Loop
while true do
    if not getgenv().paused then
        local fruits = game:GetService("Workspace"):GetDescendants()
        local fruitMaisProximo = nil
        local distanciaMaisProxima = math.huge

        -- Encontra o fruit mais próximo
        for _, objeto in pairs(fruits) do
            if objeto ~= nil and objeto.Name == getgenv().fruitParaFarmar then
                local distancia = (objeto.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
                if distancia < distanciaMaisProxima then
                    distanciaMaisProxima = distancia
                    fruitMaisProximo = objeto
                    break
                end
            end
        end

        -- Ataca o fruit
        if game.Players.LocalPlayer.Character.Humanoid.Level >= getgenv().levelMinimo and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
            if fruitMaisProximo and distanciaMaisProxima <= getgenv().distanciaDeAtaque then
                game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Attacking)
                task.wait(getgenv().tempoDeAtaque)
                game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Running)
            else
                game.Players.LocalPlayer.Character.Humanoid:MoveTo(fruitMaisProximo.Position)
            end
        end
    end

    task.wait(getgenv().tempoDeAtaque)
end
```
