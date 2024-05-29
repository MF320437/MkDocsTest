# EventManager System Documentation

## Introduction

The EventManager system is a modular approach to managing events in a Roblox game. It consists of the following modules:

1. **EventManager (Main Module)**: The main module that delegates tasks to the child modules.
2. **ClientEventManager (Child Module)**: Handles client-specific events.
3. **ServerEventManager (Child Module)**: Handles server-specific events.
4. **Utilities (Optional Child Module)**: Provides common utility functions.

This documentation will guide you through the usage and implementation details of each module.

## Module Documentation

1. [EventManager (Main Module)](EventManager.md)
2. [ClientEventManager (Child Module)](clienteventmanager.md)
3. ServerEventManager (Child Module) - ***documentation unfinished***
4. Utilities (Optional Child Module) - ***documentation unfinished***

## Usage Examples

Here are some examples of how to use the EventManager system:

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