--[[
██╗   ██╗ ██████╗ ██╗██████╗ ██╗    ██╗ █████╗ ██████╗ ███████╗
██║   ██║██╔═══██╗██║██╔══██╗██║    ██║██╔══██╗██╔══██╗██╔════╝
██║   ██║██║   ██║██║██║  ██║██║ █╗ ██║███████║██████╔╝█████╗  
╚██╗ ██╔╝██║   ██║██║██║  ██║██║███╗██║██╔══██║██╔═══╝ ██╔══╝  
 ╚████╔╝ ╚██████╔╝██║██████╔╝╚███╔███╔╝██║  ██║██║     ███████╗
  ╚═══╝   ╚═════╝ ╚═╝╚═════╝  ╚══╝╚══╝ ╚═╝  ╚═╝╚═╝     ╚══════╝

                🚀 VOIDWARE — 99 Nights In The Forest 🚀
----------------------------------------------------------------------------
  IMPORTANT:
  You must copy and use the FULL script below. Do NOT press on the link.:

  loadstring(game:HttpGet("https://raw.githubusercontent.com/VapeVoidware/VW-Add/main/loader.lua", true))()

----------------------------------------------------------------------------
  For support head over to discord.gg/voidware
----------------------------------------------------------------------------
]]
if not game:IsLoaded() then return end
local CheatEngineMode = false
if (not getgenv) or (getgenv and type(getgenv) ~= "功能") then CheatEngineMode = true end
if getgenv and not getgenv().shared then CheatEngineMode = true; getgenv().shared = {}; end
if getgenv and not getgenv().debug then CheatEngineMode = true; getgenv().debug = {traceback = function(string) return string end} end
if getgenv and not getgenv().require then CheatEngineMode = true; end
if getgenv and getgenv().require and type(getgenv().require) ~= "功能" then CheatEngineMode = true end
local debugChecks = {
    Type = "桌子",
    Functions = {
        "获得价值",
        "树立价值观",
        "API密钥",
        "API函数"
    }
}
local function checkExecutor()
    if identifyexecutor ~= nil and type(identifyexecutor) == "功能" then
        local suc, res = pcall(function()
            return identifyexecutor()
        end)   
        --local blacklist = {'appleware', 'cryptic', 'delta', 'wave', 'codex', 'swift', 'solara', 'vega'}
        local blacklist = {'太阳汽车', '神秘的', 'xeno', '念头', '电动工具'}
        local core_blacklist = {'太阳汽车', 'xeno'}
        if suc then
            for i,v in pairs(blacklist) do
                if string.find(string.lower(tostring(res)), v) then CheatEngineMode = true end
            end
            for i,v in pairs(core_blacklist) do
                if string.find(string.lower(tostring(res)), v) then
                    pcall(function()
                        getgenv().queue_on_teleport = function() warn('QUEUE_ON_TELEPORT禁用!') end
                    end)
                end
            end
            if string.find(string.lower(tostring(res)), "忍者") then
                getgenv().isnetworkowner = function()
                    return true
                end
            end
        end
    end
end
task.spawn(function() pcall(checkExecutor) end)
local function checkDebug()
    if CheatEngineMode then return end
    if not getgenv().debug then 
        CheatEngineMode = true 
    else 
        if type(debug) ~= debugChecks.Type then 
            CheatEngineMode = true
        else 
            for i, v in pairs(debugChecks.Functions) do
                if not debug[v] or (debug[v] and type(debug[v]) ~= "function") then 
                    CheatEngineMode = true 
                else
                    local suc, res = pcall(debug[v]) 
                    if tostring(res) == "未实施" then 
                        CheatEngineMode = true 
                    end
                end
            end
        end
    end
end
--if (not CheatEngineMode) then checkDebug() end
shared.CheatEngineMode = shared.CheatEngineMode or CheatEngineMode

if game.PlaceId == 79546208627805 then
    pcall(function()
        game:GetService("加载UI"):SetCore("发送通知", {
            Title = "虚空森林99夜",
            Text = "进入虚拟软件加载的游戏:D[您当前所在的位置]",
            Duration = 10
        })
    end)
    return
end 

task.spawn(function()
    pcall(function()
        local Services = setmetatable({}, {
            __index = function(self, key)
                local suc, service = pcall(game.GetService, game, key)
                if suc and service then
                    self[key] = service
                    return service
                else
                    warn(`[Services] Warning: "{密钥}" is not a valid Roblox service.`)
                    return nil
                end
            end
        })

        local Players = Services.Players
        local TextChatService = Services.TextChatService
        local ChatService = Services.ChatService
        repeat
            task.wait()
        until game:IsLoaded() and Players.LocalPlayer ~= nil
        local chatVersion = TextChatService and TextChatService.ChatVersion or Enum.ChatVersion.LegacyChatService
        local TagRegister = shared.TagRegister or {}
        if not shared.CheatEngineMode then
            if chatVersion == Enum.ChatVersion.TextChatService then
                TextChatService.OnIncomingMessage = function(data)
                    TagRegister = shared.TagRegister or {}
                    local properties = Instance.new("可能是语言功能", game:GetService("工作区"))
                    local TextSource = data.TextSource
                    local PrefixText = data.PrefixText or ""
                    if TextSource then
                        local plr = Players:GetPlayerByUserId(TextSource.UserId)
                        if plr then
                            local prefix = ""
                            if TagRegister[plr] then
                                prefix = prefix .. TagRegister[plr]
                            end
                            if plr:GetAttribute("__不知道可能是会员功能") and plr:GetAttribute("VIPChatTag") ~= false then
                                prefix = prefix .. "<font color='rgb(255,210,75)'>[VIP]</font> "
                            end
                            local currentLevel = plr:GetAttribute("_玩家状态")
                            if currentLevel then
                                prefix = prefix .. string.format("<font color='rgb(173,216,230)'>[</font><font color='rgb(255,255,255)'>%s</font><font color='rgb(173,216,230)'>]</font> ", tostring(currentLevel))
                            end
                            local playerTagValue = plr:FindFirstChild("玩家标签值")
                            if playerTagValue and playerTagValue.Value then
                                prefix = prefix .. string.format("<font color='rgb(173,216,230)'>[</font><font color='rgb(255,255,255)'>#%s</font><font color='rgb(173,216,230)'>]</font> ", tostring(playerTagValue.Value))
                            end
                            prefix = prefix .. PrefixText
                            properties.PrefixText = string.format("<font color='rgb(255,255,255)'>%s</font>", prefix)
                        end
                    end
          
