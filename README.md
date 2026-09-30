# OSGames UI
<p align="center">
  <img src="https://i.imgur.com/ndFlWEu.png" width="49%" alt="Home tab" />
  <img src="https://i.imgur.com/sj991Ag.png" width="49%" alt="Settings tab" />
</p>
<p align="center">
  <img src="https://i.imgur.com/IeW4tdV.png" width="320" alt="Notification" />
</p>
Lightweight Matcha Drawing UI. Right Shift toggles by default.

## Load UI

```lua
local URL = "https://raw.githubusercontent.com/DontRunSean/OSGamesRoblox/refs/heads/main/OSGames.lua"
local src = httpget(URL)
local fn = loadstring(src)
pcall(fn)
local UI = getfenv().OSGames or rawget(_G, "OSGames")
```

## Quick start | example tab

```lua
local tab = UI:AddTab({Title = "Main", Icon = "bolt"})

tab:AddButton({
  Title = "Give speed",
  Description = "Sets WalkSpeed to 100",
  ButtonText = "Run",
  Callback = function()
    local lp = game:GetService("Players").LocalPlayer
    local hum = lp.Character and lp.Character:FindFirstChild("Humanoid")
    if hum then hum.WalkSpeed = 100 end
  end
})

tab:AddToggle({
  Title = "Auto farm",
  Description = "Runs while on",
  Default = false,
  Callback = function(v)
    print("toggle:", v)
  end
})
```

New tabs insert above Settings automatically. Use `tab:Select()` to switch to a tab.

## Controls

All take `Title`, `Description`, `Icon`. Return a control with `GetValue()` / `SetValue(v)` / `SetText(t)` / `SetDescription(t)`.

```lua
tab:AddButton({Title = "Hi", Description = "...", ButtonText = "Run", Callback = function() end})
tab:AddToggle({Title = "Hi", Default = false, Callback = function(v) end})
tab:AddSlider({Title = "Hi", Min = 0, Max = 100, Step = 1, Default = 50, Callback = function(v) end})
tab:AddDropdown({Title = "Hi", Options = {"A", "B", "C"}, Default = "A", Callback = function(v) end})
tab:AddKeybind({Title = "Hi", Description = "..."})
tab:AddLabel("Just text")
tab:AddLabel({Title = "Hi", Description = "..."})
```

Toggle loop pattern:

```lua
local running = false
tab:AddToggle({
  Title = "Loop",
  Default = false,
  Callback = function(v)
    running = v
    if not v then return end
    task.spawn(function()
      while running and UI.Alive do
        -- work here
        task.wait(0.5)
      end
    end)
  end
})
```

## Menu settings

```lua
UI:SetTheme("Black")     -- Purple, Green, Blue, Black, Red, Orange, Cyan, Pink
UI:SetKeybind(0xA1)      -- Right Shift. 0xA0 Left Shift, 0x2D Insert, etc.
UI:Notify({Title = "Hi", Content = "it works", Type = "success", Duration = 4})
UI:RequestClose()        -- shows unload confirm
UI:Destroy()             -- unloads immediately
```

Useful flags: `UI.Visible`, `UI.BgOpacity` (0.2–1), `UI.RGBSpin`, `UI.Effects`, `UI.EffectStrength`.

## Icons

`Icon = "..."` on any tab or control. Unknown names fall back to `script`.

Available (18):

`spark`, `layers`, `bolt`, `shield`, `palette`, `power`, `sliders`, `home`, `close`, `script`, `down`, `up`, `left`, `right`, `check`, `key`, `info`, `gear`

Defaults: button = `bolt`, toggle = `power`, slider = `sliders`, dropdown = `layers`, keybind = `key`, label = `spark`.

## Notes

- Matcha only. Needs the Drawing API.
- Client code is always copyable once running (`decompile` / `getscripts` can dump it). Obfuscation only slows people down. Keep secrets server-side.
