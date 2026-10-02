<p align="center">
  <img src="https://i.imgur.com/ndFlWEu.png" width="49%" alt="Home tab" />
  <img src="https://i.imgur.com/sj991Ag.png" width="49%" alt="Settings tab" />

A lightweight, clean external UI library for Roblox (Matcha).

**Default toggle key:** Right Shift

---

## Features

- Smooth animations & modern look
- 8 built-in themes
- Tabs + sidebar navigation
- Buttons, Toggles, Sliders, Dropdowns, Keybinds, Labels
- Notifications
- Per-control hotkeys (right-click any button/toggle to bind)
- Draggable window
- Avatar display
- Easy unload with confirmation

---

## Requirements

- **Matcha** executor (or any executor with the Drawing API)
- Internet access (for avatar + loading)

---

## How to Load

```lua
local URL = "https://raw.githubusercontent.com/DontRunSean/OSGamesRoblox/refs/heads/main/OSGames.lua"
local src = httpget(URL)
local fn = loadstring(src)
pcall(fn)

local UI = getfenv().OSGames or rawget(_G, "OSGames")
```

After loading, the menu appears. Press **Right Shift** to show/hide it.

---

## Quick Example (Template Menu)

```lua
-- Load the library first (see above)

-- Create a new tab
local Main = UI:AddTab({
    Title = "Main",
    Icon = "bolt"
})

-- Button
Main:AddButton({
    Title = "Kill All",
    Description = "Example button",
    ButtonText = "Run",
    Callback = function()
        print("Button clicked!")
    end
})

-- Toggle
Main:AddToggle({
    Title = "Auto Farm",
    Description = "Example toggle",
    Default = false,
    Callback = function(value)
        print("Toggle is now:", value)
    end
})

-- Slider
Main:AddSlider({
    Title = "WalkSpeed",
    Description = "Change your speed",
    Min = 16,
    Max = 200,
    Step = 1,
    Default = 16,
    Callback = function(value)
        local hum = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
        if hum then
            hum.WalkSpeed = value
        end
    end
})

-- Dropdown
Main:AddDropdown({
    Title = "Select Mode",
    Description = "Choose an option",
    Options = {"Easy", "Normal", "Hard", "Impossible"},
    Default = "Normal",
    Callback = function(value)
        print("Selected:", value)
    end
})

-- Keybind (custom)
Main:AddKeybind({
    Title = "Custom Keybind",
    Description = "Click to set a key"
})

-- Label
Main:AddLabel({
    Title = "Info",
    Description = "This is just a text label"
})

-- Optional: switch to the new tab
Main:Select()
```

---

## All Controls

| Control     | Example |
|-------------|---------|
| **Button**  | `tab:AddButton({Title = "...", Description = "...", ButtonText = "Run", Callback = function() end})` |
| **Toggle**  | `tab:AddToggle({Title = "...", Default = false, Callback = function(v) end})` |
| **Slider**  | `tab:AddSlider({Title = "...", Min = 0, Max = 100, Step = 1, Default = 50, Callback = function(v) end})` |
| **Dropdown**| `tab:AddDropdown({Title = "...", Options = {"A","B","C"}, Default = "A", Callback = function(v) end})` |
| **Keybind** | `tab:AddKeybind({Title = "...", Description = "..."})` |
| **Label**   | `tab:AddLabel({Title = "...", Description = "..."})` or `tab:AddLabel("Just text")` |

Every control returns an object with:
- `:GetValue()`
- `:SetValue(value)`
- `:SetText(text)`
- `:SetDescription(text)`
- `:SetHotkey(vk)` / `:ClearHotkey()`

---

## Useful Functions

```lua
UI:SetTheme("Purple")          -- Purple, Green, Blue, Black, Red, Orange, Cyan, Pink
UI:SetKeybind(0xA1)            -- Change menu toggle key (Right Shift by default)
UI:Notify({
    Title = "Success",
    Content = "It works!",
    Type = "success",          -- "info", "success", "error"
    Duration = 4
})
UI:Minimize()                  -- Hide the window
UI:Show()                      -- Show the window
UI:Toggle()                    -- Toggle visibility
UI:RequestClose()              -- Show unload confirmation
UI:Destroy()                   -- Instantly unload everything
```

### Useful Flags

```lua
UI.Visible = true/false
UI.BgOpacity = 0.85            -- 0.2 to 1.0
UI.RGBSpin = true              -- Rainbow border
UI.Effects = true
UI.EffectStrength = 0.8
UI.ReducedMotion = false
```

---

## Icons

You can set `Icon = "name"` on any tab or control.

**Available icons:**
`spark` · `layers` · `bolt` · `shield` · `palette` · `power` · `sliders` · `home` · `close` · `script` · `down` · `up` · `left` · `right` · `check` · `key` · `info` · `gear`

---

## Notes

- New tabs are automatically placed above the Settings tab.
- Right-click any Button or Toggle to bind a personal hotkey.
- The library cleans up after itself when you unload.

---

**Credits**
- Original UI ideas: 9mfg
- Source inspiration: objectivizing
- Current maintainer: DontRunSean
```
<p align="center">
  <img src="https://i.imgur.com/IeW4tdV.png" width="320" alt="Notification" />
</p>

[README.md](https://github.com/user-attachments/files/32953504/README.md)
