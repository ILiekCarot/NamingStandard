# Console

The **console** functions are used to interact with one console window.

Behavior and examples documented on this page are based on Script-Ware.

---

## consoleclear

```lua
function consoleclear(): ()
```

Clears the output of the console window.

### Example

```lua
-- Create the console window
consolesettitle("New console")
consoleprint("Hello, world!")
consolecreate()

-- Clears the output "Hello, world!"
consoleclear()
```

---

## consolecreate

```lua
function consolecreate(): ()
```

Opens the console window. Text previously output to the console will not be cleared.

> ### 🔎 Note
> Some executors also allow functions like `consoleprint` to open the console.\
> This is confusing behavior that should not be relied on.

### Example

Create a program that generates a mountainous landscape:

```lua
-- Create the console window
consolesettitle("Beautiful Mountains")
consolecreate()

local function generate()
	-- Generate a random decimal number for noise
	local seed = math.random(100, 999) + math.random()

	-- Prints 25 lines of text
	for i = 1, 25 do
		local noise = math.noise(i / 8, seed) + 0.5
		local height = math.floor(noise * 50)
		local line = string.rep("*", height)
		consoleprint(line .. "\n")
	end

	-- Prompts the user to generate a new set of mountains
	-- or exit the console window
	consoleprint("\nEnter 'Y' to generate a new landscape, or nothing to exit\n")

	local input = consoleinput()

	if string.lower(input) == "y" then
		consoleclear()
		generate()
	else
		consoledestroy()
	end
end

generate()
```

---

## consoledestroy

```lua
function consoledestroy(): ()
```

Closes the console window and clears its output. The title will not be changed.

### Example

```lua
-- Create a console window titled "New console" and with the output "Hello, world!"
consolesettitle("New console")
consoleprint("Hello, world!")
consolecreate()

-- Close the console window, clearing its output
consoledestroy()

-- Reopen the console window titled "New console" with no output
consolecreate()
```

---

## consoleinput

`⏰ Yields`

```lua
function consoleinput(): string
```

Waits for the user to input text into the console window. Returns the result.

### Example

```lua
-- Create the console window
consolesettitle("Your Info")
consoleprint("What is your name?\nMy name is: ")
consolecreate()

-- Retrieve the user's input
local name = consoleinput()
consoleprint("Hello, " .. name .. "!")

-- Cleanup
task.wait(1)
consoledestroy()
```

---

## consoleprint

```lua
function consoleprint(text: string): ()
```

Prints `text` to the console window. Does not clear existing text or create a new line.

### Parameters

* `text` - The text to append to the output.

### Example

```lua
-- Create a console window titled "New console" with the
-- output "Hello, world!! How are you today?"
consolesettitle("New console")
consoleprint("Hello, world!")
consoleprint("! How are you today?")
consolecreate()
```

---

## consolesettitle

```lua
function consolesettitle(title: string): ()
```

Sets the title of the console window to `title`.

### Parameters

 * `title` - The new title.

### Aliases

 * `consolename`

### Example

```lua
-- Create a console window titled "My console"
consolesettitle("My console")
consolecreate()
```