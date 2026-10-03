<p align="center">
  <img src="https://i.imgur.com/nMT48Ah.png" width="49%" alt="Home tab" />
</p>

A lightweight, clean external UI library for Roblox (Matcha).

**Default toggle key:** Right Shift

---

## Features

- Smooth animations & modern look
- 8 built in themes
- Tabs + sidebar navigation
- Buttons, Toggles, Sliders, Dropdowns, Keybinds, Labels
- **Two column sections** (`AddSection`) with headers + middle divider
- **Per toggle colors** + global Colored toggles switch
- **Primary** full-width action bars and **Row** whole row buttons
- Whole row toggle clicks (switch, text, anywhere on the row)
- Notifications
- Per control hotkeys (right click any button/toggle to bind, hints on every row)
- Draggable window
- Avatar display
- Easy unload with confirmation / should unload all scripts ran {not guaranteed} 

---

## Requirements

- **Matcha**  (or any external with the Drawing API but lets be real its matcha or nothin) nurd... nvm
- Internet access (for avatar + loading) -_-

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

> Load order: run the library **first**, then your menu script. Scripts written
> for older versions keep working unchanged (same `AddTab`/`AddToggle`/…
> calls, same `UI.Tabs`, `Notify`, `OnUnload`).

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

## Two-Column Sections

```lua
local main = UI:AddTab({ Title = "Main", Icon = "home" })

-- Left column
local tp = main:AddSection({ Title = "TELEPORT", Column = 1 })
tp:AddButton({ Title = "Teleport To Home", Icon = "home", ButtonText = "Go",
    Row = true, Callback = function() end })

-- Right column
local esp = main:AddSection({ Title = "ESP", Column = 2 })
esp:AddToggle({ Title = "ESP Players", Default = true,
    Color = Color3.fromRGB(170, 130, 255) })
```

- Section titles render as accent headers; a divider appears when both columns are used.
- Plain `tab:Add*` controls keep rendering full-width, so old scripts are unaffected.
- `tab:SetColumns(1)` forces single-column mode.

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

Extra options (all optional, all backwards compatible):

| Option     | Where | What |
|------------|-------|------|
| `Color`    | Toggle, Slider | `Color3` on-state color (toggle falls back to green, slider to accent) |
| `Primary`  | Button | Full-width dark action bar with the title inside it |
| `Row`      | Button | Clicking anywhere on the row fires it (toggles always behave this way) |
| `Column`   | Any control | `1` / `2` to place it without a section |
| `Hotkey`   | Button, Toggle | Preset hotkey (`"G"`, `"F1"`, …) |
| `Icon`     | Tab, any control | Icon name (see below) |

Every control returns an object with:
- `:GetValue()`
- `:SetValue(value)`
- `:SetText(text)`
- `:SetDescription(text)`
- `:SetColor(color)` / `:GetColor()`
- `:SetHotkey(vk)` / `:ClearHotkey()`

Titles on buttons and toggles cut off at 20 characters (`...`).

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
UI.BgOpacity = 0.85            -- fixed look, no slider
UI.RGBSpin = true              -- Rainbow border
UI.Effects = true
UI.EffectStrength = 0.8
UI.ReducedMotion = false
UI.ColoredToggles = true       -- green/custom on-states (Settings tab)
UI.SidebarHover = false        -- true = sidebar collapses until moused over
```

---

## Settings Tab

Ships with the library: Theme picker, Colored toggles, Sidebar hover
expand, Menu keybind recorder, RGB spin, notification test.

---

## Icons

You can set `Icon = "name"` on any tab or control. Unknown names fall back
to `script`.

**Available icons:**
`spark` · `layers` · `bolt` · `shield` · `palette` · `power` · `sliders` · `home` · `close` · `script` · `down` · `up` · `left` · `right` · `check` · `key` · `info` · `gear`

`bolt` tints yellow, `power` green, `home` blue, plus muted tones for
`sliders` / `layers` / `gear`.

---

## Notes

- New tabs are automatically placed above the Settings tab.
- Right click any Button or Toggle to bind a personal hotkey (hint on each row).
- Control hotkeys fire even while the menu is hidden.
- The library cleans up after itself when you unload.

---

**Credits**
- Original UI ideas: 9mfg
- Source inspiration: objectivizing
- Current maintainer: DontRunSean
