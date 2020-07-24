# FiveM-ImageHost
Just a few instructions on setting up a image host to upload and view images, compatible with the screenshot basic resource for FiveM.


## Required Repos
<https://github.com/hauxir/imgpush>

Setup as per the instructions within its readme.md. 


# Utilized by the Screenshot-basic resources
Client Side:
```lua
exports['screenshot-basic']:requestScreenshotUpload(server, 'file', {encoding = 'png', quality = 0.88}, function(data)
    print(data)
    local t = json.decode(data) -- returns a table
    local link = format.string('%s/%s',server,t.filename)

    TriggerEvent('chat:addMessage', { template = '<img src="{0}" style="width: 50%; height: 43%;" />', args = {link} })
end)
```
