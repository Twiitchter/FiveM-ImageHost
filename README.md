# FiveM-ImageHost
Just a few instructions on setting up a image host to upload and view images, compatible with the screenshot basic resource for FiveM.


## Required Repos
<https://github.com/hauxir/imgpush>

Setup as per the instructions within its readme.md. 

*Forked when confirmed working at time of testing*
<https://github.com/Twiitchter/imgpush>

### Utilized by the Screenshot-basic resources
Client Side:
```lua
RegisterNetEvent('Test')
AddEventHandler('Test', function()
local server =  'http://THE.IPADDRESS.OFYOUR.IMAGESERVER:5000'
--
exports['screenshot-basic']:requestScreenshotUpload(server, 'file', {encoding = 'png', quality = 0.88}, function(data)
    print(data)
    --
    local t = json.decode(data) -- returns a table
    local link = format.string('%s/%s',server,t.filename)
    --
    TriggerEvent('chat:addMessage', { template = '<img src="{0}" style="width: 50%; height: 43%;" />', args = {link} })
end)
end)
---
RegisterCommand('Screenshot', function() TriggerEvent('Test') end, false) 
RegisterKeyMapping('Screenshot', 'Testing', 'keyboard', '/') -- Keybind Default(Menu/Settings/Keybinds/FiveM)..
```

Server Side:
```lua
-- Inside event to be triggered... 
local id = source
local server =  'http://THE.IPADDRESS.OFYOUR.IMAGESERVER:5000'
-- You could try localhoast:port, but I have not done so. 

exports['screenshot-basic']:requestClientScreenshot(id, {encoding = 'png', quality = 0.88}, function(err, data)
    -- if error else false
    print('err', err)
    -- return filename as json. 
    print('data', data)
    --
    local t = json.decode(data) -- returns a table
    local link = format.string('%s/%s',server,t.filename)
    TriggerClientEvent('chat:addMessage', id, { template = '<img src="{0}" style="width: 50%; height: 43%;" />', args = {link} }) 
end)
```
