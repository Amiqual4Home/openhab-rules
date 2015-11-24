This is a rule recently to control my smathome with "natural" voice commands (using openhab HABdroid). I wanted to be able to add/remove or change commands very fast, so it's based on a combination or rule and map transform files.
It's for french (with a weird mix of english), but just changing (or adding) commands in the map files will work as well. A big advantage of the map transform files is that it's in use the second you save it. It's also great to easily increase the number of word the system will react to.
(like lamp, lamps, light, lights...)

To use it you must send a command to the "VoiceCommand" item (like the HABroid app does).

It can be like "Put the lights on in the kitchen"

The place is determined looking for matches in the reco_room.map file (first found, first used). This file contains matchings beetween room names and the room openhab Groups from your items.
Then the item "VoiceCommand_loc" is called with a command like "room:command" (here : "Kitchen:Switch the lights on in the kitchen" (the purpose is that you can call it directly from a device specific to a room).

The deviceType (and sometimes specific device) is determined using the reco_device.map file.
You can describe a matching for a group/deviceType (for example lamp=Lights) or a specific item from the deviceType (like banana=Lights.BananaLamp).

The command is then found in a the specific reco_action_<deviceType>.map file ( for example, reco_action_Lights.map for Lights or Lights.BananaLamp).

After that, if the device is specific (like BananaLamp), the command will be send only to this item.
If it's a deviceType (like Lights), the command will be send to all the members of the group from the specific room group (like Kitchen).
If no room was found, the command will be send to all the members of the deviceType group in all the house.

It's very simple yet quite powerfull when you understand how to use it, and very easy to configure by adding constantly new maps.
Another cool thing is that a command can also be in the device map.
For example "red" will be in the reco_action_hueColor.map (red=360,100,50), but also in the reco_device.map (red=hueColor).
That way if you say "I want some red" or even just "red", all your items in the hueColor group will receive the command "360,100,50".

I also made a specific thing for increase and decrease, since not every dimmer items (with knx and other) can handle this. If you put "INCREASE_20" or "DECREASE_10" in the command for example, the rule will send a command to increase or decrease from the specified ammount.
If no number is specified, it will just send INCREASE or DEACREASE.

This is a very raw first shot, but you can really have a lot of fun with it (and I do :p).