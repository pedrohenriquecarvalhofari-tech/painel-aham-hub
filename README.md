-- AHAM HUB ADM WHITELIST

local Players = game:GetService("Players")
local LP = Players.LocalPlayer

-- =========================
-- WHITELIST
-- =========================

local whitelist = {

["ajudo_pessoas21"] = true,
["ninja_branco02"] = true

}

local dono = "ajudo_pessoas21"

function isWhitelisted(player)

return whitelist[player.Name] == true

end

-- se não tiver whitelist não roda

if not isWhitelisted(LP) then

return

end

-- =========================
-- CHAT
-- =========================

local mensagem = "Painel ADM do Aham Hub executado com sucesso"

pcall(function()

game:GetService("TextChatService")
.TextChannels.RBXGeneral
:SendAsync(mensagem)

end)

print(mensagem)

-- =========================
-- TAG
-- =========================

function criarTag()

local char = LP.Character or LP.CharacterAdded:Wait()

local head = char:WaitForChild("Head")

local tag = Instance.new("BillboardGui")
tag.Parent = head

tag.Size = UDim2.new(0,200,0,50)
tag.StudsOffset = Vector3.new(0,2,0)
tag.AlwaysOnTop = true

local text = Instance.new("TextLabel",tag)

text.Size = UDim2.new(1,0,1,0)
text.BackgroundTransparency = 1
text.TextScaled = true

if LP.Name == dono then

text.Text = "DONO DO AHAM HUB"
text.TextColor3 = Color3.fromRGB(255,200,0)

else

text.Text = "ADM DO AHAM HUB"
text.TextColor3 = Color3.fromRGB(0,255,255)

end

end

criarTag()

LP.CharacterAdded:Connect(function()

wait(1)

criarTag()

end)

-- =========================
-- FUNÇÕES
-- =========================

local targetPlayer = nil
local loopkill = false

function getPlayer(nome)

for i,v in pairs(Players:GetPlayers()) do

if string.lower(v.Name):sub(1,#nome) == string.lower(nome) then
return v
end

end

end

-- =========================
-- COMANDOS
-- =========================

LP.Chatted:Connect(function(msg)

local args = msg:split(" ")

-- KILL

if args[1] == ";kill" then

targetPlayer = getPlayer(args[2])

if targetPlayer then
targetPlayer.Character:BreakJoints()
end

end

-- LOOPKILL

if args[1] == ";loopkill" then

targetPlayer = getPlayer(args[2])
loopkill = true

end

-- UNLOOPKILL

if args[1] == ";unloopkill" then

loopkill = false

end

-- KICK

if args[1] == ";kick" then

targetPlayer = getPlayer(args[2])

if targetPlayer then

targetPlayer:Kick("Você foi banido pela equipe Aham Hub")

end

end

end)

-- LOOPKILL

task.spawn(function()

while true do

task.wait(1)

if loopkill and targetPlayer then

if targetPlayer.Character then
targetPlayer.Character:BreakJoints()
end

end

end

end)

-- =========================
-- GUI
-- =========================

local gui = Instance.new("ScreenGui")
gui.Parent = game.CoreGui

local frame = Instance.new("Frame",gui)

frame.Size = UDim2.new(0,320,0,260)
frame.Position = UDim2.new(0.4,0,0.3,0)

frame.BackgroundColor3 = Color3.fromRGB(0,0,0)

frame.Active = true
frame.Draggable = true

Instance.new("UICorner",frame)

-- RGB

task.spawn(function()

while true do

for i=0,1,0.01 do

frame.BorderColor3 = Color3.fromHSV(i,1,1)

task.wait()

end

end

end)

-- TITULO

local title = Instance.new("TextLabel",frame)

title.Size = UDim2.new(1,0,0,40)
title.BackgroundTransparency = 1
title.Text = "AHAM HUB ADM"
title.TextScaled = true
title.TextColor3 = Color3.new(1,1,1)
