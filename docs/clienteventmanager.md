# ClientEventManager (Child Module)

The `ClientEventManager` module is responsible for handling client-specific events in a Roblox game. It provides a set of functions to register, fire, and unregister client events, ensuring a consistent and organized way of managing event-driven interactions on the client-side.

## Module Structure

The `ClientEventManager` module has the following structure:

```lua
-- ClientEventManager Module
local ClientEventManager = {}

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local clientEvents = {}

local function getOrCreateEvent(eventTable, eventName)
    -- Implementation to get or create a RemoteEvent in ReplicatedStorage
end

function ClientEventManager.RegisterClientEvent(eventName, callback, priority)
    -- Implementation to register a client event
end

function ClientEventManager.FireClientEvent(eventName, ...)
    -- Implementation to fire a client event
end

function ClientEventManager.UnregisterClientEvent(eventName, callback)
    -- Implementation to unregister a client event
end

return ClientEventManager
```

## Functions

### `getOrCreateEvent(eventTable, eventName)`

This function is responsible for getting or creating a `RemoteEvent` in the `ReplicatedStorage` service for a given event name.

**Parameters:**
- `eventTable`: A table that stores the registered client events.
- `eventName`: The name of the event.

**Returns:**
- A table containing the `RemoteEvent` and a table of registered callbacks for the event.

### `ClientEventManager.RegisterClientEvent(eventName, callback, priority)`

This function allows you to register a client event with a callback function and an optional priority.

**Parameters:**
- `eventName`: The name of the event.
- `callback`: The function to be called when the event is fired.
- `priority`: (Optional) The priority of the callback function. Higher priority callbacks will be executed first.

**Usage Example:**
```lua
local EventManager = require(game.ReplicatedStorage.EventManager)

local function onClientHit()
    print("Client hit event received")
end

EventManager.Client.RegisterClientEvent("OnClientHit", onClientHit)
```

### `ClientEventManager.FireClientEvent(eventName, ...)`

This function allows you to fire a client event with optional arguments.

**Parameters:**
- `eventName`: The name of the event to be fired.
- `...`: (Optional) Any arguments to be passed to the registered callbacks.

**Usage Example:**
```lua
local EventManager = require(game.ReplicatedStorage.EventManager)

EventManager.Client.FireClientEvent("OnClientHit")
```

### `ClientEventManager.UnregisterClientEvent(eventName, callback)`

This function allows you to unregister a client event callback.

**Parameters:**
- `eventName`: The name of the event.
- `callback`: The function to be unregistered.

**Usage Example:**
```lua
local EventManager = require(game.ReplicatedStorage.EventManager)

local function onClientHit()
    print("Client hit event received")
end

EventManager.Client.RegisterClientEvent("OnClientHit", onClientHit)
-- Later, when you want to unregister the event
EventManager.Client.UnregisterClientEvent("OnClientHit", onClientHit)
```

## Integrating with Utilities Module

The `ClientEventManager` module can be integrated with an optional `Utilities` module, which provides a `SortByPriority` function to sort the registered callbacks by their priority.

```lua
-- ClientEventManager Module (with Utilities)
local ClientEventManager = {}
local Utilities = require(script.Parent.Utilities)

function ClientEventManager.RegisterClientEvent(eventName, callback, priority)
    local eventEntry = getOrCreateEvent(clientEvents, eventName)
    table.insert(eventEntry.callbacks, {callback = callback, priority = priority or 0})
    Utilities.SortByPriority(eventEntry.callbacks)
    eventEntry.event.OnClientEvent:Connect(function(...)
        for _, cb in ipairs(eventEntry.callbacks) do
            cb.callback(...)
        end
    end)
end

return ClientEventManager
```

In this updated version, the `RegisterClientEvent` function uses the `Utilities.SortByPriority` function to sort the registered callbacks by their priority, ensuring that higher priority callbacks are executed first.

## Conclusion

The `ClientEventManager` module provides a robust and flexible way to manage client-specific events in a Roblox game. By using this module, you can easily register, fire, and unregister events, ensuring a consistent and organized event-driven architecture on the client-side.