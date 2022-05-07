_G.Setting_table = {
    Auto_Farm = false,
    FastAttack = true
}

getgenv()['MyName'] = game.Players.LocalPlayer.Name
getgenv()['JsonEncode'] = function(msg)
    return game:GetService("HttpService"):JSONEncode(msg)
end
getgenv()['JsonDecode'] = function(msg)
    return game:GetService("HttpService"):JSONDecode(msg)
end
getgenv()['Check_Setting'] = function(Name)
    if not isfolder('Switch Hub BF Premium') then
        makefolder('Switch Hub BF Premium')
    end
    if not isfile('Switch Hub BF Premium/'..Name..'.json') then
        writefile('Switch Hub BF Premium/'..Name..'.json',JsonEncode(_G.Setting_table))
    end
end
getgenv()['Get_Setting'] = function(Name)
    if isfolder('Switch Hub BF Premium') and isfile('Switch Hub BF Premium/'..Name..'.json') then
        _G.Setting_table = JsonDecode(readfile('Switch Hub BF Premium/'..Name..'.json'))
        return _G.Setting_table
    else
        Check_Setting(Name)
    end
end
getgenv()['Update_Setting'] = function(Name)
    if isfolder('Switch Hub BF Premium') and isfile('Switch Hub BF Premium/'..Name..'.json') then
        writefile('Switch Hub BF Premium/'..Name..'.json',JsonEncode(_G.Setting_table))
    else
        Check_Setting(Name)
    end
end

Check_Setting(getgenv()['MyName'])
Get_Setting(getgenv()['MyName'])

_G.wl_key = _G.Setting_table.Key
loadstring(game:HttpGet('https://switch-hub.store/script.lua'))()
