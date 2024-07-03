# Instances

The **Instance** functions are used to interact with game objects and their properties.

---

## getcallbackvalue

```lua
function getcallbackvalue(object: Instance, property: string): function?
```

Returns the function assigned to a callback property of `object`, which cannot be indexed normally.

### Parameters

 * `object` - The object to get the callback property from.
 * `property` - The name of the callback property.

### Example

```lua
local bindable = Instance.new("BindableFunction")

function bindable.OnInvoke()
	print("Hello, world!")
end

print(getcallbackvalue(bindable, "OnInvoke")) --> function()
print(bindable.OnInvoke) --> Throws an error
```

---

## getconnections

```lua
function getconnections(signal: ENCScriptSignal): {Connection}
--ENCScriptSignal is an ENC alternative to RBXScriptSignal
```

Creates a list of Connection objects for the functions connected to `signal`.

### Connection

| Field | Type | Description |
| ----- | ---- | ----------- |
| `Enabled` | boolean | Whether the connection can receive events. |
| `ForeignState` | boolean | Whether the function was connected by a foreign Luau state (i.e. CoreScripts). |
| `LuaConnection` | boolean | Whether the connection was created in Luau code. |
| `Function` | function? | The function bound to this connection. Nil when `ForeignState` is true. |
| `Thread` | thread? | The thread that created the connection. Nil when `ForeignState` is true. |

| Method | Description |
| ----- | ----------- |
| `Fire(...: any): ()` | Fires this connection with the provided arguments. |
| `Defer(...: any): ()` | [Defers](https://devforum.roblox.com/t/beta-deferred-lua-event-handling/1240569) an event to connection with the provided arguments. |
| `Disconnect(): ()` | Disconnects the connection. |
| `Disable(): ()` | Prevents the connection from firing. |
| `Enable(): ()` | Allows the connection to fire if it was previously disabled. |

### Parameters

 * `signal` - The signal to retrieve connections from.

### Example

```lua
local connections = getconnections(game.DescendantAdded)

for _, connection in ipairs(connections) do
	connection:Disable()
end
```

---

## gethiddenproperty

```lua
function gethiddenproperty(object: Instance, property: string): (any, boolean)
```

Returns the value of a hidden property of `object`, which cannot be indexed normally.

If the property is hidden, the second return value will be `true`. Otherwise, it will be `false`.

### Parameters

 * `object` - The object to index.
 * `property` - The name of the hidden property.

### Example

```lua
local fire = Instance.new("Fire")
print(gethiddenproperty(fire, "size_xml")) --> 5, true
print(gethiddenproperty(fire, "Size")) --> 5, false
```

---

## gethui

```lua
function gethui(): Folder
```

Returns a hidden GUI container. Should be used as an alternative to CoreGui and PlayerGui.

GUI objects parented to this container will be protected from common detection methods.

### Example

```lua
local gui = Instance.new("ScreenGui")
gui.Parent = gethui()
```

---

## getinstances

```lua
function getinstances(): {Instance}
```

Returns a list of every Instance referenced on the client.

### Example

```lua
local objects = getinstances()

local gameCount = 0
local miscCount = 0

for _, object in ipairs(objects) do
	if object:IsDescendantOf(game) then
		gameCount += 1
	else
		miscCount += 1
	end
end

print(gameCount) --> The number of objects in the `game` hierarchy.
print(miscCount) --> The number of objects outside of the `game` hierarchy.
```

---

## getnilinstances

```lua
function getnilinstances(): {Instance}
```

Like `getinstances`, but only includes Instances that are not descendants of a service provider.

### Example

```lua
local objects = getnilinstances()

for _, object in ipairs(objects) do
	if object:IsA("LocalScript") then
		print(object, "is a LocalScript")
	end
end
```

---

## isscriptable

`🪲 Compatibility`

```lua
function isscriptable(object: Instance, property: string): boolean
```

Returns whether the given property is scriptable (does not have the `notscriptable` tag).

If `true`, the property is scriptable and can be indexed normally. If `nil`, the property does not exist.

> ### 🪲 Known Issues
> Ion know what this shit does, so I wont give u an example.

### Parameters

 * `object` - The object to index.
 * `property` - The name of the property.

---

## sethiddenproperty

```lua
function sethiddenproperty(object: Instance, property: string, value: any): boolean
```

Sets the value of a hidden property of `object`, which cannot be set normally. Returns whether the property was hidden.

### Parameters

 * `object` - The object to index.
 * `property` - The name of the hidden property.
 * `value` - The value to set.

### Example

```lua
local fire = Instance.new("Fire")
print(sethiddenproperty(fire, "Size", 5)) --> false (not hidden)
print(sethiddenproperty(fire, "size_xml", 15)) --> true (hidden)
print(gethiddenproperty(fire, "size_xml")) --> 15, true (hidden)
```

---

## setscriptable

`🪲 Compatibility`

```lua
function setscriptable(object: Instance, property: string, value: boolean): boolean
```

Set whether the given property is scriptable. Returns whether the property was scriptable prior to changing it.

> ### 🪲 Known Issues
> This appears to be backwards on Script-Ware. An example will not be provided until behavior is consistent.

### Parameters

 * `object` - The object to index.
 * `property` - The name of the property.
 * `value` - Whether the property should be scriptable.