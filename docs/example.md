# Example

The `UI Dropdown` component comes with a working example that shows you a simple setup along with an example of how to use the events system.

Drag and drop the `UI Dropdown Example` template into your hierarchy.  This example already has a client context and UI container setup.

Enter play mode and test the 2 drop downs.

![](images/preview.png)

## Example Script

```lua
-- Text UI components to show what was picked

local fruit_text = script:GetCustomProperty("fruit_text"):WaitForObject()
local apple_text = script:GetCustomProperty("apple_text"):WaitForObject()

-- Our dropdown has the event set to "fruit".
-- Here we update the text with the fruit selected and if it's the Apple, then 
-- we broadcast an event to enable the Apple Type dropdown.

Events.Connect("on_fruit_selected", function(index, option, value)
	fruit_text.text = "You picked " .. option.text .. "!"

	if(option.text == "Apple") then
		Events.Broadcast("on_apple_type_enable")
	else
		Events.Broadcast("on_apple_type_disable", true)
		apple_text.text = ""
	end
end)

-- The other dropdown event and text updating

Events.Connect("on_apple_type_selected", function(index, option, value)
	apple_text.text = "You picked " .. option.text .. "!"
end)

-- Grab the local player

local local_player = Game.GetLocalPlayer()

-- Show cursor and allow UI to be intereacted with on player join.

Game.playerJoinedEvent:Connect(function()
	UI.SetCursorVisible(true)
	UI.SetCanCursorInteractWithUI(true)
end)
```