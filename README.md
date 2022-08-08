# Coffee-Buffs-Progressbar-Speed
Made by Sunny Scripts
Discord: https://discord.gg/WK7nYmDhrN (24/7 support and updates)
Tebex: https://sunny-scripts.tebex.io/
Kofi:https://ko-fi.com/sunnyscripts

# Description

- **Drinking coffees make all your progressbar faster for a duration of time set.**

Feel free to let me know how it should be done better ;)
Check out my store above for more NoPixel inspired scripts and support.
Love you all.

Inspired by Project Sloth's spirits <3

# Installation

# 1.

- **Go to qb-smallresources> client> consumables.lua and _CTRL+F / FIND_ `RegisterNetEvent('consumables:client:Drink', function(itemName)`**

- **REPLACE FROM**

  ```lua
      TriggerEvent("inventory:client:ItemBox", QBCore.Shared.Items[itemName], "remove")
      TriggerEvent('animations:client:EmoteCommandStart', {"c"})
      TriggerServerEvent("QBCore:Server:SetMetaData", "thirst", QBCore.Functions.GetPlayerData().metadata["thirst"] + ConsumeablesDrink[itemName])
  ```

- **TO**

```lua
        TriggerEvent("inventory:client:ItemBox", QBCore.Shared.Items[itemName], "remove")
        if itemName == 'coffee' then
            TriggerEvent("progressbar:client:faster", 30)
        end
        TriggerEvent('animations:client:EmoteCommandStart', {"c"})
        TriggerServerEvent("QBCore:Server:SetMetaData", "thirst", QBCore.Functions.GetPlayerData().metadata["thirst"] + ConsumeablesDrink[itemName])
```

---

# 2.

- **GO TO progressbar > client > main.lua, ADD this anywhere at the top**

```lua
local faster = false
local time = 0

local function Buff(time)
    local t = time * 60
    CreateThread(function ()
        while true do
            if t > 0 then
                faster = true
            else
                faster = false
                break
            end
            Wait(1000)
        end
    end)
end
RegisterNetEvent("progressbar:client:faster", function (time)
    Buff(time)
end)
```

- **FIND `function Process(action, start, tick, finish)` and REPLACE THIS**

  ```lua
  SendNUIMessage({
  action = "progress",
  duration = Action.duration,
  label = Action.label
  })
  ```

* **TO THIS**
  ```lua
  local dur = Action.duration
  if faster == true then
    dur = (Action.duration * 2) / 10
  else
    dur = Action.duration
  end
  SendNUIMessage({
  action = "progress",
  duration = dur,
  label = Action.label
  })
  ```

```

```
