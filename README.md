# Priz's UI Library

A modern, animated Roblox UI library with smooth transitions, beautiful theming, and advanced UI components.

## Features

✨ **Smooth Animations**
- Fade in/out effects on all UI elements
- Button click animations with bounce effect
- Tab switching with slide animations (right to left)
- Smooth hover effects with color shifts

🎨 **Beautiful Design**
- Clean, modern interface with rounded corners
- Dynamic theme system with multiple built-in themes
- Smooth color transitions
- Professional typography with GothamBold font

🔧 **Advanced Components**
- Toggles with smooth state transitions
- Sliders with custom formatting
- Dropdowns with search functionality
- Color pickers with transparency support
- Key bindings with multiple modes

❄️ **Special Effects**
- Falling snow animation contained within the UI
- Soft glow effects on hover
- Button press animations

## Installation

```lua
local repo = "https://raw.githubusercontent.com/PrizLovesRice1/UILibrary/main/"
local Library = loadstring(game:HttpGet(repo .. "Library.lua"))()
local ThemeManager = loadstring(game:HttpGet(repo .. "addons/ThemeManager.lua"))()
local SaveManager = loadstring(game:HttpGet(repo .. "addons/SaveManager.lua"))()
```

## Quick Start

```lua
-- Create a window
local Window = Library:CreateWindow({
    Title = "Priz's Hub",
    Footer = "version: 1.0",
    Icon = 95816097006870,
    NotifySide = "Right",
    ShowCustomCursor = true,
})

-- Add a tab
local MainTab = Window:AddTab("Main", "user")

-- Add a groupbox
local GroupBox = MainTab:AddLeftGroupbox("My Features", "boxes")

-- Add a toggle
GroupBox:AddToggle("MyToggle", {
    Text = "Feature Toggle",
    Default = false,
    Callback = function(Value)
        print("Toggle value:", Value)
    end,
})

-- Access the toggle value
if Toggles.MyToggle.Value then
    print("Feature is enabled!")
end
```

## Main Components

### Windows
Create the main UI window with customizable settings.

```lua
local Window = Library:CreateWindow({
    Title = "Your Hub Name",
    Footer = "version: 1.0",
    Icon = 0, -- Leave as 0 for text icon
    Size = UDim2.fromOffset(720, 600),
    Position = UDim2.fromOffset(6, 6),
    Center = true,
    Resizable = true,
})
```

### Tabs
Organize features into tabs for better UI structure.

```lua
local Tab = Window:AddTab("Tab Name", "icon-name")
-- Icons from: https://lucide.dev/
```

### Groupboxes
Group related features together.

```lua
local GroupBox = Tab:AddLeftGroupbox("Group Name", "icon-name")
-- Or add to the right side:
local GroupBox = Tab:AddRightGroupbox("Group Name", "icon-name")
```

### Toggle/Checkbox
Boolean state controls.

```lua
GroupBox:AddToggle("IndexName", {
    Text = "Display Text",
    Default = false,
    Tooltip = "Hover text",
    Callback = function(Value)
        -- Called when toggled
    end,
})

-- Access value
if Toggles.IndexName.Value then
    -- Do something
end

-- Listen for changes
Toggles.IndexName:OnChanged(function()
    print("Toggle changed to:", Toggles.IndexName.Value)
end)
```

### Sliders
Numeric value selection.

```lua
GroupBox:AddSlider("SliderName", {
    Text = "Slider Label",
    Default = 50,
    Min = 0,
    Max = 100,
    Rounding = 1,
    Callback = function(Value)
        print("Slider value:", Value)
    end,
})

-- Access value
local Value = Options.SliderName.Value
```

### Dropdowns
Select from multiple options.

```lua
GroupBox:AddDropdown("DropdownName", {
    Values = { "Option1", "Option2", "Option3" },
    Default = 1,
    Multi = false, -- Set to true for multiple selection
    Searchable = true,
    Callback = function(Value)
        print("Selected:", Value)
    end,
})
```

### Buttons
Interactive action buttons.

```lua
GroupBox:AddButton({
    Text = "Button Text",
    Func = function()
        print("Button clicked!")
    end,
    DoubleClick = false, -- Requires double-click to execute
    Tooltip = "Hover text",
})
```

### Input/Textbox
User text input.

```lua
GroupBox:AddInput("InputName", {
    Default = "Default text",
    Text = "Input Label",
    Placeholder = "Enter text...",
    Numeric = false, -- true for numbers only
    Callback = function(Value)
        print("Input:", Value)
    end,
})
```

### Color Picker
Select colors with transparency.

```lua
GroupBox:AddLabel("Color"):AddColorPicker("ColorName", {
    Default = Color3.new(1, 0, 0),
    Title = "Color Picker",
    Transparency = 0, -- Set to > 0 to enable transparency
    Callback = function(Value)
        print("Color:", Value)
    end,
})
```

### Key Picker
Select keyboard keybinds.

```lua
GroupBox:AddLabel("Keybind"):AddKeyPicker("KeyName", {
    Default = "E",
    Mode = "Toggle", -- or "Hold", "Press", "Always"
    Text = "Keybind",
    Callback = function(Value)
        print("Key pressed:", Value)
    end,
})
```

## Animations

### Smooth Transitions
All UI changes use smooth fade and slide animations:
- **Fade in/out**: Elements smoothly appear and disappear
- **Slide**: Content slides from right to left when switching tabs
- **Hover glow**: Buttons and toggles glow when hovered
- **Click bounce**: Buttons shrink and bounce when clicked

### Snow Effect
The library includes an optional falling snow effect contained within the UI window:
- Particles fade in smoothly
- Snow stays within window bounds
- No overlap with UI elements
- Customizable particle count and speed

## Theming

Switch between built-in themes or create custom ones.

```lua
-- Set a built-in theme
ThemeManager:ApplyToTab(Tabs["UI Settings"])

-- Available themes: Default, BBot, Fatality, Jester, Mint, Tokyo Night, Ubuntu, Quartz, Nord, Dracula, Monokai, Gruvbox, Solarized
```

## Saving Configurations

Automatically save and load user settings.

```lua
-- Setup SaveManager
SaveManager:SetLibrary(Library)
SaveManager:SetFolder("MyHub/Config")
SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({ "MenuKeybind" })
SaveManager:BuildConfigSection(Tabs["UI Settings"])

-- Load auto-save config
SaveManager:LoadAutoloadConfig()
```

## Profile Section

Add a custom profile section at the bottom-left:

```lua
-- Profile is automatically added with avatar and name
-- Customize in the Library window creation
```

## Performance Tips

1. Use callbacks for heavy operations asynchronously
2. Disable custom cursor if experiencing lag
3. Limit animations on lower-end devices
4. Use `Library:OnUnload()` for cleanup

```lua
Library:OnUnload(function()
    print("Library unloaded!")
    -- Cleanup code here
end)
```

## API Reference

### Window Methods
- `Window:AddTab(Name, Icon)` - Create a new tab
- `Window:AddKeyTab(Name)` - Create a key binding tab
- `Window:SetCornerRadius(Radius)` - Set corner roundness
- `Window:SetFooter(Text)` - Update footer text

### Tab Methods
- `Tab:AddLeftGroupbox(Name, Icon)` - Add groupbox on left
- `Tab:AddRightGroupbox(Name, Icon)` - Add groupbox on right
- `Tab:AddLeftTabbox()` - Create nested tabs on left
- `Tab:AddRightTabbox()` - Create nested tabs on right

### Groupbox Methods
- `Groupbox:AddToggle(Index, Options)` - Add toggle
- `Groupbox:AddCheckbox(Index, Options)` - Add checkbox
- `Groupbox:AddSlider(Index, Options)` - Add slider
- `Groupbox:AddDropdown(Index, Options)` - Add dropdown
- `Groupbox:AddButton(Options)` - Add button
- `Groupbox:AddInput(Index, Options)` - Add textbox
- `Groupbox:AddLabel(Text, DoesWrap)` - Add label
- `Groupbox:AddDivider()` - Add divider line

## Support

For issues, questions, or feature requests, visit:
https://github.com/PrizLovesRice1/UILibrary

## License

This library is provided as-is for use in Roblox games.

---

**Made by Priz** ✨
