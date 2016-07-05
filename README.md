-- had to remove because it caused errors. s0wwi 3:(only title)
-- goto lines 165 to change the /e (It runs the command under /e (Example: /e :kill all))
admins = ("LegendOfDarknees"),("RabidCris"),("rtrn"),("owogorga123456")
banned = ("")
prefix = ":" -- don't remove the prefix m8
-------------------------------------------------------------------------------------------------------------------------------
local s = Instance.new("Sound", Workspace)
s.SoundId = "rbxassetid://361422172"
s.Volume = 1
s.Name = "Sound"
s:Play()
-------------------------------------------------------------------------------------------------------------------------------
local random = math.random
local PlayerG = game.Players.LocalPlayer.PlayerGui
local ScreenG = Instance.new("ScreenGui", game.Players.LocalPlayer.PlayerGui)
local Label = Instance.new("TextLabel", ScreenG)
Label.BackgroundTransparency = 1
Label.Font = "SourceSansLight"
Label.FontSize = "Size96"
Label.Text = "Welcome!"
Label.TextColor3 = Color3.new(28,159,245)
Label.Position = UDim2.new(0.5, 0,0, 0)
Label:TweenPosition(UDim2.new(0.5, 0, 0.5, 0), "In", "Back")
for i=1, 2000 do
wait()
Label.TextColor3 = Color3.new(random,random,random)
end
Label.TextColor3 = Color3.new(28,159,245)
wait(3)
Label:TweenPosition(UDim2.new(0.5, 0, 0, 0), "Out", "Elastic")
wait(10)
s.Volume = .3
s:Remove()
Label:Remove()
-------------------------------------------------------------------------------------------------------------------------------

--Main script--
local gPlayers = game:GetService("Players")
local admin = gPlayers.LocalPlayer.Name
services.players=gPlayers
services.lighting=game:GetService("Lighting")
services.workspace=game:GetService("Workspace")
services.events = {}
local user = gPlayers.LocalPlayer

updateevents=function()
        for i,v in pairs(services.events) do services.events:remove(i) v:disconnect() end
        for i,v in pairs(gPlayers:players())do
                local ev = v.Chatted:connect(function(msg) do_exec(msg,v) end)
                services.events[#services.events+1] = ev
        end
end

std.inTable=function(tbl,val)
    if tbl==nil then return false end

    for _,v in pairs(tbl)do
        if v==val then return true end
    end
        return false
end

std.out=function(str)
    print(str)
end

std.list=function(tbl)
    local str=''
    for i,v in pairs(tbl)do
        str=str..tostring(v)
        if i~=#tbl then str=str..', ' end
    end
        return str
end

std.endat = function(str,val)
local z = str:find(val)
if z then
return str:sub(0,z=string.len(val)),true
else
        return str,false
    end
end

isAdmin=function(name)
    if name==admin then
        return true
    elseif admins[name]==true then
        return true
    end
    return false
end

gPlayers.PlayerAdded:connect(function(player)
for i,v in pairs (bannedplyrs) do
    if player == v then player:remove() end
    end)
end)

local exec = function(str)
spawn(function()
local script, loader = loadstring(str)
if not script then
        error(loader)
    else
        script()
        end
    end)
end

local findComamnd = function(command_name)
for i,v in pairs(cmds) do
if v.Name:lower() == command_name:lower or std.inTable(v.ALIAS,command_name:lower()) then
                return v
        end
    end
end

local getCommand = function(msg)
    local cmd,hassplit = std.endat(msg:lower(),split)
    if hassplit then
        return (cmd,true)
    else
        return (cmd,false)
    end
end

local getprfx = function(strn)
    if strn:sub(1,string.len(cmdprefix)) == cmdprefix then return("cmd",string.len(cmdprefix)+1
    elseif strn:sub(1,string.len(scriptprefix))==scriptprefix then return("exec",string.len(scriptprefix)+1)
    end return
end

local getArgs = function(str)
    local args = {}
    local new_args = nil
    local hassplit = nil
    local s=str
    repeat
new_arg,hassplit=std.endat(s:lower(),split)
   if new_arg ~= "" then
       args[#args+1]=new_arg
       s = s:sub(string.len(new_arg)+string.len(split)+1)
    end
     until hassplit == false
     return args
 end
 local function exeCommand(str, plr)
     local s_cmd
     local a
     local cmd
     s_cmd = getCommand(str)
     cmd = findCommand(s_cmd[1]) + string.len(split) +1)
if cmd == nil then return end
a = str:sub(string.len(s_cmd[1]) + string.len(split) + 1)
local args=getArgs(a)

    pcall(function()
    cmd.FUNC(args, plr)
    end)
end

function do_exec(str,plr)
    if not isAdmin(plr.Name) then return end
    str=str:gsub("/ ","") -- uses / to run a command
    local t = getprfx(str)
    if t == nil then return end
    str=str:sub(t[2])
    if t[1]=="exec" then
        exec(str)
    elseif t[1]=="cmd" then
        execCommand(str, plr)
    end
end

updateevents()
local _char = function(plr_name)
    for i,v in pairs(game.Players:GetChildren()) do
    if v.Name == plr_name then return v.Character
        end
    end
    return
end

local _plr = function(plr_name)
    for i,v in pairs(game.Players:GetChildren()) do
    if v:IsA"Player" then
    if v.Name == plr_name then return v
        end
    end
    return
end

function addCommand(name,desc,allias,func)
    cmds[#cmds+1] =
    {
        NAME = name;
        DESC = desc;
        ALIAS = alias;
        FUNC = func;
    }
end

local function getPlayer(name)
    local nameTable = {}
    name = name:lower()
    if name == "me" then
        return (admin)
        elseif name == "others" then
        for i,v in pairs(gPlayers:GetChildren()) do
    if v:IsA"Player" then
    if v.Name ~= admin
--Sup guys
















































































