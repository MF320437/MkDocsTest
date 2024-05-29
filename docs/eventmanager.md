# EventManager (Main Module)

The `EventManager` is the main module that serves as the entry point for managing events in a Roblox game. It acts as a central hub, delegating tasks to its child modules: `ClientEventManager` and `ServerEventManager`. The `EventManager` also provides an optional `Utilities` module for common utility functions.

## Modules

### `EventManager` (Main Module)

The `EventManager` module is responsible for requiring and delegating tasks to the child modules.

```lua
-- EventManager Module
local EventManager = {}

local ClientEventManager = require(script.ClientEventManager)
local ServerEventManager = require(script.ServerEventManager)

EventManager.Client = ClientEventManager
EventManager.Server = ServerEventManager

return EventManager
```

### `ClientEventManager` (Child Module)

The `ClientEventManager` module handles client-specific events. It provides functions to register, fire, and unregister client events.

```lua
-- ClientEventManager Module
local ClientEventManager = {}

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local clientEvents = {}

local function getOrCreateEvent(eventTable, eventName)
    -- Code to get or create a RemoteEvent in ReplicatedStorage
end

function ClientEventManager.RegisterClientEvent(eventName, callback, priority)
    -- Code to register a client event with the specified callback and priority
end

function ClientEventManager.FireClientEvent(eventName, ...)
    -- Code to fire a client event
end

function ClientEventManager.UnregisterClientEvent(eventName, callback)
    -- Code to unregister a client event
end

return ClientEventManager
```

### `ServerEventManager` (Child Module)

The `ServerEventManager` module handles server-specific events. It provides functions to register, fire, and unregister server events, as well as a function to handle client-to-server events.

```lua
-- ServerEventManager Module
local ServerEventManager = {}

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local serverEvents = {}

local function getOrCreateEvent(eventTable, eventName)
    -- Code to get or create a BindableEvent in ReplicatedStorage
end

function ServerEventManager.RegisterServerEvent(eventName, callback, priority)
    -- Code to register a server event with the specified callback and priority
end

function ServerEventManager.FireServerEvent(eventName, ...)
    -- Code to fire a server event
end

function ServerEventManager.UnregisterServerEvent(eventName, callback)
    -- Code to unregister a server event
end

function ServerEventManager.HandleClientToServerEvent(eventName, callback)
    -- Code to handle a client-to-server event
end

return ServerEventManager
```

### `Utilities` (Optional Child Module)

The `Utilities` module contains common utility functions that can be used by both the `ClientEventManager` and `ServerEventManager` modules.

```lua
-- Utilities Module
local Utilities = {}

function Utilities.SortByPriority(callbacks)
    -- Code to sort a table of callbacks by priority
end

return Utilities
```

## Usage Examples

### Client Script

```lua
local EventManager = require(game.ReplicatedStorage.EventManager)

local function onClientHit()
    print("Client hit event received")
end

EventManager.Client.RegisterClientEvent("OnClientHit", onClientHit)

-- Unregister the client event
-- EventManager.Client.UnregisterClientEvent("OnClientHit", onClientHit)
```

### Server Script

```lua
local EventManager = require(game.ReplicatedStorage.EventManager)

local function onAbilityUsed(player, ability)
    print(player.Name .. " used ability: " .. ability)
end

EventManager.Server.RegisterServerEvent("OnAbilityUsed", onAbilityUsed)

-- Handle client-to-server event
EventManager.Server.HandleClientToServerEvent("OnAbilityUsed", onAbilityUsed)

-- Unregister the server event
-- EventManager.Server.UnregisterServerEvent("OnAbilityUsed", onAbilityUsed)
```

## Functions

### `EventManager.Client`

The `EventManager.Client` table provides access to the `ClientEventManager` module, allowing you to register, fire, and unregister client-specific events.

### `EventManager.Server`

The `EventManager.Server` table provides access to the `ServerEventManager` module, allowing you to register, fire, and unregister server-specific events, as well as handle client-to-server events.

### `ClientEventManager.RegisterClientEvent(eventName, callback, priority)`

Registers a client-specific event with the given `eventName`, `callback` function, and optional `priority` value. The `priority` value determines the order in which the callbacks are executed, with higher priority values being executed first.

### `ClientEventManager.FireClientEvent(eventName, ...)`

Fires a client-specific event with the given `eventName` and any additional arguments.

### `ClientEventManager.UnregisterClientEvent(eventName, callback)`

Unregisters a client-specific event with the given `eventName` and `callback` function.

### `ServerEventManager.RegisterServerEvent(eventName, callback, priority)`

Registers a server-specific event with the given `eventName`, `callback` function, and optional `priority` value. The `priority` value determines the order in which the callbacks are executed, with higher priority values being executed first.

### `ServerEventManager.FireServerEvent(eventName, ...)`

Fires a server-specific event with the given `eventName` and any additional arguments.

### `ServerEventManager.UnregisterServerEvent(eventName, callback)`

Unregisters a server-specific event with the given `eventName` and `callback` function.

### `ServerEventManager.HandleClientToServerEvent(eventName, callback)`

Handles a client-to-server event with the given `eventName` and `callback` function.

### `Utilities.SortByPriority(callbacks)`

Sorts a table of callbacks by their `priority` values in descending order.

## Conclusion

The `EventManager` module provides a centralized and modular approach to managing events in a Roblox game. By separating client-specific and server-specific events into their respective child modules, the `EventManager` promotes code organization and maintainability. The optional `Utilities` module further enhances the functionality by providing common utility functions.