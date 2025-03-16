# Loadstring
```lua
local WindUI = loadstring(game:HttpGet("https://tree-hub.vercel.app/api/UI/WindUI"))()
```

# Window
```lua
local Window = WindUI:CreateWindow({
    Title = "WindUI Library",
    Icon = "door-open",
    Author = "Example UI",
    Folder = "CloudHub",
    Size = UDim2.fromOffset(580, 460),
    Transparent = true,
    Theme = "Dark",
    SideBarWidth = 200,
    --Background = "rbxassetid://13511292247", -- rbxassetid only
    HasOutline = false,
    -- remove it below if you don't want to use the key system in your script.
    KeySystem = { 
        Key = { "1234", "5678" },
        Note = "The Key is '1234' or '5678",
        -- Thumbnail = {
        --     Image = "rbxassetid://18220445082", -- rbxassetid only
        --     Title = "Thumbnail"
        -- },
        URL = "https://github.com/Footagesus/WindUI", -- remove this if the key is not obtained from the link.
        SaveKey = true, -- optional
    },
})
```

# Hide And Show Ui
```lua
Window:EditOpenButton({
    Title = "Open Example UI",
    Icon = "monitor",
    CornerRadius = UDim.new(0,10),
    StrokeThickness = 2,
    Color = ColorSequence.new( -- gradient
        Color3.fromHex("FF0F7B"), 
        Color3.fromHex("F89B29")
    ),
    --Enabled = false,
    Draggable = true,
})
```

# Tabs
```lua
local Tabs = {
    ButtonTab = Window:Tab({ Title = "Button", Icon = "mouse-pointer-2", Desc = "Contains interactive buttons for various actions." }),
    CodeTab = Window:Tab({ Title = "Code", Icon = "code", Desc = "Displays and manages code snippets." }),
}
```

```lua
Window:SelectTab(1)
```

# Normal Button
```lua
Tabs.ButtonTab:CreateButton({
    Title = "Click Me",
    Desc = "This is a simple button",
    Callback = function() 
        print("Button Clicked!") 
    end
})
```

# Lock Button
```lua
Tabs.ButtonTab:CreateButton({
    Title = "Locked Button",
    Desc = "This button is locked",
    Locked = true
}
```

# Unlock Button
```lua
Tabs.ButtonTab:CreateButton({
    Title = "Submit",
    Desc = "Click to submit",
    Callback = function() 
        print("Submitted!") 
    end,
    Locked = false
})
```

# Code Tab
```lua
Tabs.CodeTab:Code({
    Title = "Example Code",
    Code = [[

local message = "Hello"
print(message)

if message == "Hello" then
    print("Greetings!")
end
    ]],
})
```

# Color Picker
```lua
Tabs.ColorPickerTab:CreateColorpicker({
    Title = "Pick a Color",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(color) 
        print("Selected color: " .. tostring(color)) 
    end
})
```

# Background Color 
```lua
Tabs.ColorPickerTab:CreateColorpicker({
    Title = "Background Color",
    Default = Color3.fromRGB(0, 0, 255),
    Callback = function(color) 
        print("Background color: " .. tostring(color)) 
    end
})
```

# Get Notification 
```lua
Tabs.NotificationTab:CreateButton({
    Title = "Click to get Notified",
    Callback = function() 
        WindUI:Notify({
            Title = "Notification Example",
            Content = "Content",
            Icon = "droplet-off",
            Duration = 5
        })
    end
})
```

# Off Toggle
```lua
Tabs.ToggleTab:CreateToggle({
    Title = "Enable Feature",
    Default = true,
    Callback = function(state) 
        print("Feature enabled: " .. tostring(state)) 
    end
})
```

# On Toggle
```lua
Tabs.ToggleTab:CreateToggle({
    Title = "Activate Mode",
    Default = false,
    Callback = function(state) 
        print("Mode activated: " .. tostring(state)) 
    end
})
```

# Toggle With Icon
```lua
Tabs.ToggleTab:CreateToggle({
    Title = "Toggle with icon",
    Icon = "check",
    Default = false,
    Callback = function(state) 
        print("Toggle with icon activated: " .. tostring(state)) 
    end
})
```

# Volume Slider
```lua
Tabs.SliderTab:CreateSlider({
    Title = "Volume Slider",
    Min = 0,
    Max = 100,
    Default = 50,
    Callback = function(value) 
        print("Volume set to: " .. value) 
    end
})
```

# Brightness Slider
```lua
Tabs.SliderTab:CreateSlider({
    Title = "Brightness Slider",
    Min = 1,
    Max = 100,
    Default = 75,
    Callback = function(value) 
        print("Brightness set to: " .. value) 
    end
})
```

# Input Box
```lua
Tabs.InputTab:CreateInput({
    Title = "Password",
    Default = "GUEST",
    Placeholder = "Enter your password",
    Callback = function(input) 
        print("Password entered.") 
    end
})
```

# Dropdown
```lua
Tabs.DropdownTab:CreateDropdown({
    Title = "Select an Option",
    Values = { "Option 1", "Option 2", "Option 3" },
    Default = "Option 1",
    Callback = function(option) 
        print("Selected: " .. option) 
    end
})
```

-- Configuration 

# Config
```lua
local HttpService = game:GetService("HttpService")

local folderPath = "WindUI"
makefolder(folderPath)

local function SaveFile(fileName, data)
    local filePath = folderPath .. "/" .. fileName .. ".json"
    local jsonData = HttpService:JSONEncode(data)
    writefile(filePath, jsonData)
end

local function LoadFile(fileName)
    local filePath = folderPath .. "/" .. fileName .. ".json"
    if isfile(filePath) then
        local jsonData = readfile(filePath)
        return HttpService:JSONDecode(jsonData)
    end
end

local function ListFiles()
    local files = {}
    for _, file in ipairs(listfiles(folderPath)) do
        local fileName = file:match("([^/]+)%.json$")
        if fileName then
            table.insert(files, fileName)
        end
    end
    return files
end

Tabs.WindowTab:Section({ Title = "Window" })

local themeValues = {}
for name, _ in pairs(WindUI:GetThemes()) do
    table.insert(themeValues, name)
end
```
