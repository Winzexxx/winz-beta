local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local mouse = player:GetMouse()

-- Установите начальную скорость
local normalSpeed = 16
local flyingSpeed = 100

-- Обработчик для изменения скорости
function onKeyPress(input)
    if input.KeyCode == Enum.KeyCode.Z then
        humanoid.WalkSpeed = flyingSpeed
    elseif input.KeyCode == Enum.KeyCode.X then
        humanoid.WalkSpeed = normalSpeed
        character.HumanoidRootPart.Anchored = true
        local bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.Velocity = (mouse.Hit.p - character.HumanoidRootPart.Position).unit * flyingSpeed
        bodyVelocity.Parent = character.HumanoidRootPart
        wait(0.1)
        bodyVelocity:Destroy()
        character.HumanoidRootPart.Anchored = false
    end
end

-- Подписка на событие ввода
game:GetService("UserInputService").InputBegan:Connect(onKeyPress)
