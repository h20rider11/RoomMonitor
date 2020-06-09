Skip to content
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@h20rider11 
Learn Git and GitHub without any code!
Using the Hello World guide, you’ll start a branch, write comments, and open a pull request.



 Code
 Issues 9
 Pull requests 4 Actions
 Projects 0
 Wiki
 Security 0
 Insights
h20rider11 random code stuff for smartthings
 559 commits
 4 branches
 0 packages
 0 releases
 4 contributors
 GPL-3.0
Latest commit
@adey
adey v1.0.1 driver
Latest commit
5974894
on Jan 14
Files
Type	Name	Latest commit message	Commit time
app	v5.2.0	13 months ago
devicetypes/h20rider11/rooms-occupancy.src	v1.0.1 driver	5 months ago
driver	v1.0.1 driver	5 months ago
resources	Add files via upload	2 years ago
smartapps/bangali	v1.0.1	5 months ago
.gitignore	v0.99.0	2 years ago
CHANGELOG.md	v1.0.1	5 months ago
LICENSE	Initial commit	3 years ago
README.md	v0.70.0	2 years ago
 README.md
bangali's rooms automation


Rooms Manager: Smarter Rooms: Personalized home automation with Occupancy
Features:
Here is a summary of features for the quick reader.
Rooms settings:
Set room occupancy state for each room, using any or all of the following devices:
Presence sensors.
Motion sensors.
Contact sensors.
Music players.
Button pushes.
Switches on and off.
Power wattage.
Create rules that evaluate:
For all rules:
Room occupancy state
Hub mode
Day of week
Lux value
Humidity range
Date filter
Time trigger
For temperature rules additionally:
Temperature
Rules allow you to:
For execution rules:
Turn on and off lights / switches.
Auto adjust level and color temperature when turning on lights.
Set light color when turning on.
Setup recurring schedules for holiday light show including annually recurring holidays.
On Hubitat, send any command to any device.
Run pistons.
Run routines.
Start and stop music players.
Set window shade position.
For temperature rules:
Maintain room temperature with thermostat or in-room AC and heaters.
Turn fan on/off and manage fan speed with room temperature.
Control vents with room temperature.
Other settings:
Setup multiple color routines for holiday light shows.
Announce when:
Contact sensor stays open.
Outside door is opened.
Turn on night lights with motion while room state is asleep.
Turn on outdoor lights on a daily schedule.
Rooms occupancy device settings:
Set alarm to play on a daily or weekly schedule for each room.
Rooms manager settings:
Check and announce:
Device battery status.
Device health monitoring status.
Announce:
Arrival and departure by name including with randomly selected greetings.
Time every quarter, half or on the hour.
Sunrise and sunset.
Announcements support speakers and / or lights.
Github updated notification.
Occupancy states, settings and other details:
While ST has a concept of rooms it is essentially a grouping mechanism which does not enable personalized automation. In contrast rooms occupancy considers the room as a meta device and automates common tasks associated with a “room” physical or virtual. What makes it really useful is not just the room's occupancy state but the ability to manage automation for rooms in a set of rules for the room based on the occupancy state of the room and data from various sensors. When creating a room device through the smartapp you are able to create these rules for the rooms making your rooms really smart.

You can continue reading here for the summarized version or read the more detailed and always the latest version on Github which also describes the individual settings:

Rooms Manager and Rooms Occupancy readme on Github

What these rules enable is many common tasks around rooms which most users go through automating at some point. Usually through setting up a few rules or using a few pistons. I have been there and done that myself. While those work to a degree it requires creating a set of rules and/or pistons to enable contextual automation per "room". As you incorporate more and more automation using rules and/or pistons these often become a maintenance challenge while still not enabling the kind of comprehensive automation that should be possible for typical devices in a room. The goal of this app is to make that possible by evaluating all sensor input from various devices in the room and enabling rules that act on these sensor values in the context of various typical automation needs in a "room".

If there is one principle that these apps are built on, it is - that your home automation should work in the background in a repeatable and predictable manner without requiring repeated human intervention. In short, your automation should work for you and not the other way around. But even more importantly perhaps, this app gets you the kind of WAF for your home automation that you have always dreamed about. 🙂

Additionally, these room occupancy devices also have attributes, capabilities and commands which are useable in webCoRE or other smartapps like Smart Lighting in ST or Rule Machine in Hubitat. There is a range of other automations that webCoRE makes possible that could not otherwise be done without writing a custom smartapp for it. I use webCoRE for that and am I big fan of Adrian. So checkout webCoRE as well if you don't already use it.

One last time, please consider continuing reading the rest of this readme on Github because that always has the most updated version:

Rooms Manager and Rooms Occupancy readme on Github

How does this app work?
This app works by setting rooms occupancy to various states based on a set of sensors as specified by the user. It takes this state and attribute values from various sensors and evaluates a set of rules that you create to match the conditions. When all of the conditions for the rule matches, it executes actions specified on these matching rules.

As an example, you can specify motion sensors in Occupied settings to set a room state to Occupied when there is motion from any of those motion sensors. Then create a rule to turn on some lights. In this rule you could also set that these lights should only be turned on if a lux sensor is at a certain lux value or lower. Or you could specify that only turn on the lights during certain times. Or you could specify turn on the lights at a certain level during certain times and at another level during other times.

As a part of the Occupied settings you can also specify timeout values so the room does not indefinitely stay set to Occupied state and the lights turn off after a while when there is no motion. How quickly that happens is controlled by you through the timeout value you specify in the settings. By specifying settings in the Checking settings you are also able to dim the lights before the lights turn off completely so there is a visual cue to the room occupant that the lights will turn off because they have not moved in a while.

Off course you may be in the room while and not be moving for a while like reading a book or watching TV. That's when you use the Engaged settings to set the room to Engaged state. See below for additional details.

Here are the common room occupancy states:

Occupied:
Occupied is you go to a room are in there for a few minutes then leave the room. Lights come on when you enter the room and turn off after a couple of minutes of your leaving the room. Think of Occupied as a transient state and Engaged below as a somewhat persistent state.


Engaged:
Engaged is when you stay in a room for an extended period of time and may be motionless for some or all of the time. since we cant depend on the motion event for engaged state there are different options to set the room to engaged for extended occupancy. these are all under engaged settings and there is more coming. but these help make sure the switches you set to on stay on even if there is no motion in the room. When in Engaged state you have a different and longer timeout state than the Occupied state. So there is still a motion requirement but a much higher time threshold than the Occupied state.


Asleep:
Asleep state is meant for use while the room should be 'asleep' as in not respond to most typical automation like motion automation. But it does allow for other automation like using a night light and using a button to turn on or off the night lights. You are still able to create rules for the Asleep state but it additionally support a little bit for Asleep state specific automation in the Asleep settings.


Vacant:
Vacant state is for when the room is vacant and you want everything to get turned off. It is possible to setup rules for Vacant settings as well but not required.


Checking:
Occupied state is used for transition between states and not user controlled. For example, when moving from Occupied to Vacant occupancy state the room will transition to Checking state. While the app does not allow creating rules for checking state there is some settings available to control dimming of the lights when in Checking state.


Locked:
Locked state disables all automations for the room and allows you to control lights and other devices in the room either manually or some other way.

The states 'locked', 'reserved', 'kaput' and 'donotdisturb' are effectively all similar in that they all disable automation. That being the case there is some sensors allowed to set / unset rooms to / from Locked state but no other automation beyond that for these occupancy states. Here is a quick description of the various top level settings and how the app works. At the heart of the app is the concept of room states and rules to automate devices based on these room's states and other sensor inputs. (In the following description when I talk about sensors it refers to devices that have attributes which are used to drive decisions in the room's rules.)

Note: Many of the following settings are optional but when specified will require other settings to be specified. Like specifying a motion sensor is optional. But if you do specify a motion sensor the motion event to trigger timeout countdown becomes required.

Top level settings:

Room Devices
Room sensors used in checking rule conditions based occupancy state and data from these sensors.

Motion sensor(s)	Room motion sensor(s) for motion activated state change like Occupied or Engaged
Motion event	Motion event to use for timeout. Choose the motion active event to start the timeout if your motion sensor does not generate a motion inactive event following the motion active event rather stays continuously active with no inactive event in between.
Room Buttons	Select up to 5 buttons all of which will allow toggling through selected states.
Selected states	Select states room buttons above will toggle through.
Presence sensor(s)	Presence sensor to associate with the room. Helps control certain room actions based on presence state
Lux sensor	Room lux sensor to use with rules for lights and switches. For some rooms specifying an outdoor sensor might work better than a room lux sensor.
Humidity sensor	Room humidity sensor to use with rules for lights and switches
Music player	Room music player to use with rules for lights and switches
Power meter	Room power sensor to use with rules for lights and switches
Window shade	Room window shade to use in rules
 

The next 6 settings group are for how the room is set to each of those 6 occupancy states and settings specific to that occupancy state.
 


Occupied Settings
Settings that specify how this occupancy state is set. Normally it is based on motion but there are also other ways of detecting Occupied state like a specific switch turning on. Available settings:

Button	Set room occupancy to Occupied state when button is pushed
Button number	Button number of button selected above
Only sets Occupied	Option to turn off toggling between Occupied and Vacant state for this button. When set to true the button will only set Occupied state and no longer toggle. This helps if you are pressing a button with no visual feedback to set the room to Occupied but accidentally press it twice and don't want the room to toggle to Vacant state when it is already in Occupied state.
Switch	Switch which when turned on will set room occupancy state to Occupied
Timeout	Value in seconds for room state timeout after last motion event
 


Engaged Settings
Settings that specify how this occupancy state is set. Normally it is based on motion but there are also other ways of detecting Engaged state like a button being pressed.

When room is busy	Set room to Engaged state if Occupied state is triggered frequently in a short period of time and the lights should stay on for longer than in Occupied state.

Counts the number of time the occupancy state changes between Engaged <> Occupied <> Checking <> Vacant within ((Occupied no motion timer + Checking dim timer) * 10).

Count = 5:  Light traffic.
Count = 7:  Medium traffic.
Count = 9:  Heavy traffic.

This is to automate Engaged state for when the room is flipping between Occupied and Vacant frequently in a short period of time.

Button	Set room occupancy to Engaged state when button is pushed
Button number	Button number of button selected above
Only sets Engaged	Option to turn off toggling between Engaged and Vacant state for this button. When set to true the button will only set Engaged state and no longer toggle. This helps if you are pressing a button with no visual feedback to set the room to Engaged but accidentally press it twice and don't want the room to toggle to Vacant state when it is already in Engaged state.
Presence sensor actions	Choose if room occupancy state should switch with presence sensor:
Arrives:   Change room occupancy to Engaged.
Departs:   Change room occupancy to Vacant.
Both:    Both of the actions.
Neither:  None of the actions.
Keep room engaged with presence	Keeps room occupancy set to Engaged when presence sensor is present
When music playing	Keeps room occupancy set to Engaged when music is playing
Switch	Switch which when turned on will set room occupancy to Engaged and when turned off will set room occupancy to Vacant.
Power value	Power value in watts which when reached will set room occupancy to Engaged
Power time range	Allows specifying time range from - to and matches to current time when evaluating power value for setting state. Supports the following values:
Sunrise:   Matches to local sunrise time with offset if specified
Sunset:    Matches to local sunset time with offset if specified
Time:     Matches to specific time/li>
Trigger from vacant	When false room will need to be in a state other than Vacant for the Asleep state to be triggered
Power stays below	Power value has to stay below power value above for this many seconds before room state timeout countdown will start. This is keep room state from changing frequently with power value fluctuating.
Contact sensor	Contact sensor(s) when closed will set room occupancy to Engaged with motion
Outside door	For use with outside doors like garage doors where the Engaged state is triggered with motion if the door is open
Does not trigger Engaged	For use with areas like landing or hallway leading to different rooms with contact sensor on those doors. You want any of the room doors opening to turn on the lights even before the landing/hallway motion sensor detects motion but you do not want these doors to set the landing/hallway to Engaged. Turn on this setting in that case.
Timeout	Value in seconds for room occupancy timeout from Engaged to Vacant
Reset Engaged/Asleep	Reset Engaged or Asleep state when another room changes to Engaged or Asleep
Reset Engaged directly	Reset room occupancy to Vacant directly without transitioning through Checking state
 


Checking Settings
Settings for timeout and light levels while in checking state.

Dim timer	Dim lights for how many seconds for visible notification of checking state and that lights and switches will be turned off.
Dim level by	If any lights are on dim them by this level.
Dim level to	If no lights are on turn them on at this level.
Lux value?	If no lights are on turn them on only when lux is at or below this lux value.
Do not restore	When transitioning from Checking state to another state do not restore the light levels to their previous value if that state is Vacant.


Vacant Settings
Settings that specify how this occupancy state is set. Normally it is based on motion but there are also other ways of detecting Occupied state like a specific switch turning off.

Button	Set room occupancy to Vacant state when button is pushed
Button number	Button number of button selected above
Switch	Switch which when turned off will set room occupancy to Vacant
Stop music	Pause music player when room occupancy changes to Vacant
 


Asleep Settings
Settings that specify how this occupancy state is set. Asleep is tricky because there is no true commonly used physical asleep sensors. So, these settings allow other ways of setting Asleep occupancy state and specifying night light settings which are a little different from how lights work through the rules.

Sleep sensor	Sleep sensor to set room occupancy to Asleep. (not a lot of device option here that supports sleep state. some users use the webCoRE presence sensor which I had originally modified to support sleep state, subsequently Adrian added the sleep state code to main.)
Button	Set room occupancy to Asleep state when button is pushed
Button number	Button number of button selected above
Only sets Asleep	Option to turn off toggling between Asleep and Vacant state for this button. When set to true the button will only set Asleep state and no longer toggle. This helps if you are pressing a button by the bedside to set the room to Asleep but accidentally press it twice and don't want the room to toggle to Vacant state when it is already in Asleep state.
Switch	Switch which when turned off will set room occupancy to Asleep
Power value	Power value in watts which when reached will set room occupancy to Asleep
Power time range	Allows specifying time range from - to and matches to current time when evaluating power value for setting state. Supports the following values:
Sunrise:   Matches to local sunrise time with offset if specified
Sunset:    Matches to local sunset time with offset if specified
Time:     Matches to specific time/li>
Trigger from vacant	When false room will need to be in a state other than Vacant for the Asleep state to be triggered
Power stays below	Power value has to stay below power value above for this many seconds before room state timeout countdown will start. This is to keep room state from changing frequently with power value fluctuating.
Timeout	Option to turn off Asleep state after certain number of hours in case you forget to turn it off in the morning. Specially useful if you do not have a contact sensor on the bedroom doors.
Reset with Contact	Option to turn off Asleep state after certain number of hours in case you forget to turn it off in the morning
Night lights:
Settings for night lights with motion while in Asleep state.

Turn on	Switches to turn on with motion while in Asleep state
Level	Set level when turning on switches above
Color temperature	Set color temperature when turning on switches above
Which motion sensors?	Pick which room motion sensors will trigger night lights when Asleep. If you multiple motion sensors in the room and only want some of them trigger night lights but not others, you can pick the ones here that should trigger night lights.
Timeout	Value in seconds for night light timeout
Button	Button to control night lights only
Button number	Button number of button selected above
Button action	Either toggle or turn night lights on or off
 


Locked Settings
Settings that specify how this occupancy state is set. This state disables all automation for the room.

Switch	Switch to set room occupancy to Locked
On or off	Set Locked state when switch turns on or turns off
Power value	Power value in watts which when reached will set room occupancy to Locked
Power time range	Allows specifying time range from - to and matches to current time when evaluating power value for setting state. Supports the following values:
Sunrise:   Matches to local sunrise time with offset if specified
Sunset:    Matches to local sunset time with offset if specified
Time:     Matches to specific time/li>
Trigger from vacant	When false room will need to be in a state other than Vacant for the Locked state to be triggered
Power stays below	Power value has to stay below power value above for this many seconds before room state timeout countdown will start. This is to keep room state from changing frequently with power value fluctuating.
Contact	Contact to set room occupancy to Locked
Open or closed	Set Locked state when contact is open or closed
Switches off	When true turn off switches when room occupancy changes to Locked
Override	When true allows use of devices in Locked state that would otherwise cause another room state to be activated.
Timeout	Option to turn off Locked state after certain number of hours
 

These group of settings allow for light routine settings used in the rules.

Auto Level 'AL' Settings
Settings to specify auto level and color temperature settings for the room which allows using 'AL' as a light level rule to automatically calculate and use these values based on time of day, wake and sleep time specified. Also allows specifying hours before and after wake and sleep times the light level and color temperature should be dimmed for optimal light levels.

Minimum level	Minimum light level
Maximum level	Maximum light level
Wakeup time	Wakeup time
Sleep time	Sleep time
Fade up to wake time	Fade light level up to wake time
Hours before	How many hours before wakeup time should light level start fading up
Hours after	How many hours after wakeup time should light level stop fading up
Fade down to sleep time	Fade light level down to sleep time
Hours before	How many hours before sleep time should light level start fading down
Hours after	How many hours after sleep time should light level stop fading down
Auto color temperature	Set color temperature along with level
Minimum kelvin	Minimum color temperature for light
Maximum kelvin	Maximum color temperature for light
Fade up to wake time	Fade color temperature up to wake time
Hours before	How many hours before wakeup time should color temperature start fading up
Hours after	How many hours after wakeup time should color temperature stop fading up
Fade down to sleep time	Fade color temperature down to sleep time
Hours before	How many hours before sleep time should color temperature start fading down
Hours after	How many hours after sleep time should color temperature stop fading down
 


Holiday Lights 'HL' Settings
Settings to specify holiday light patterns for use in rules during various holiday seasons. Allows for rotating colors through or slow twinkling any set of lights specified in the rules.

List of previously defined holiday light patterns
Option to create new holiday light pattern
Holiday Light Pattern:
Create holiday light patterns to use on different holidays or other special occasion.

Color string name	Name for this holiday light pattern for use in specifying with rules
Colors	Comma delimited list of colors
Light routine	Either Rotate or Twinkle where twinkle is a slow twinkle so the hub does not get saturated with frequent on and off commands
How many seconds	Either rotate colors or turn on and off after every how many seconds
Light level	Button to control night lights only
 

Temperature settings is their own group.

Temperature Settings
Manage temperature settings for the room in conjunction with thermostat or switch controlled room AC and/or heater. After adding temperature settings remember create temperature rules in maintain rules so the app can automate temperature control based on these rules.

Temperature sensors	Room temperature sensors
Maintain temperature	Maintain temperature:
Cool:    Cool room only
Heat:    Heat room only
Both:    Both cool and heat
Neither:  Neither
Use thermostat	Use thermostat to heat and cool or use in room AC and heater controlled by switches
Use thermostat: ON
Thermostat	Thermostat
Delta temperature	Room temperature sensor - thermostat temperature reading
Use thermostat: OFF
AC switch	Switch for in room AC
Heater switch	Switch for in room heather
Check presence	Specify presence sensors to check for presence before maintaining temperature
Check contact closed	Specify window contact sensors to check for closed before maintaining temperature
Switch override	Allow thermostat or AC / heater switch to be manually overridden for how many minutes
Outdoor temperature	Outdoor temperature sensor that is not currently used but have plans to use
Adjust temperature	Adjust cooling and heating temperature by 0.5ªF when outside temperature is respectively over 90ªF and below 32ªF
Fan switch	Fan switch to use in rules
Room vents	Room vents to automate with thermostat and room temperature.
 

Here are the rest of the settings starting with the heart of the app - Maintain Rules, which allows you to maintain automation rules for the room and turn them in to smart rooms.
 


Maintain Rules
Here's where to create the rules that check room occupancy state, various sensor values and other variables to decide which lights and switches should be turned on or off. It also allows executing a piston or routine or even starting and stopping a music player based on the rules.

List of defined rules
Option to create new rule
Edit Rule:
Add a new rule or edit existing rule settings.

Rule number	For tracking rule settings, not editable
Rule name	User defined descriptive rule name
Rule disabled	Quick way to to turn off the rule instead of editing and removing each setting for that rule
Modes	Matches to location mode when evaluating rule. Available choices are based on modes defined for that hub location
Occupancy state	Matches to current occupancy state when evaluating rule. Available choices are:
Asleep
Engaged
Occupied
Vacant:   Normally you don't need to create rules for the Vacant state. But if you want one of the lights to stay on during certain times in the evening even when the room is Vacant create a rule for the Vacant state with the right mode, times and switch(es)
Days of week	Matches to current day when evaluating rule
Rule type	Either Execution or Temperature depending on the rule type you are creating:
Execution:   Allows turning on and off switches, executing routines and pistons, starting or stopping music player and setting window shade position
Temperature:   Allows setting room temperature to maintain and room fan on and off settings
Rule type: Execution
Lux value	Matches to current lux value from sensor <= this value when evaluating rule.
Humidity range	Matches to current humidity reading from sensor
Date filter	Matches to current date when evaluating rule entered in yyyy/mm/dd format. Supports the following special values:
yyyy:   Matches to current year when evaluating rule
YYYY:   Matches to next year when evaluating rule
Time trigger	Allows specifying time range from - to and matches to current time when evaluating rule. Supports the following values:
Sunrise:   Matches to local sunrise time with offset if specified
Sunset:    Matches to local sunset time with offset if specified
Time:     Matches to specific time/li>
Turn on which lights / switches	List of devices to turn on
Set level	Level value if the light or switch being turned on supports level. Also allows picking either Auto Level or one of the Holiday Light routines defined earlier
Set color	Color to set when turning on light if the light supports color
Set color temperature	Color temperature to set when turning on light if light supports color temperature
Turn off which lights / switches	List of devices to turn off
Routines/Pistons and more:
Execute other actions.

Routines	Select routines to execute when rule evaluates as true
Piston	Select piston to execute when rule evaluates as true
Music player	Select if music player should be started or stopped when rule evaluates as true
Window shade	Set window shade to one of the preselected positions when rules evaluates as true
Timer overrides:
Override individual timer settings when this rule evaluates as true. For example normal timeout settings for Occupied state may be 180 seconds. But during Night mode the Occupied state timeout could be overridden here to be 30 seconds.

Occupied timeout	Timeout in seconds when rule evaluates as true
Engaged timeout	Timeout in seconds when rule evaluates as true
Checking timeout	Timeout in seconds when rule evaluates as true
Night light timeout	Timeout in seconds when rule evaluates as true
Rule type: Temperature
Time trigger	Allows specifying time range from - to and matches to current time when evaluating rule. Supports the following values:
Sunrise:   Matches to local sunrise time with offset if specified
Sunset:    Matches to local sunset time with offset if specified
Time:     Matches to specific time/li>
Manage room temperature settings:

Cool temperature	Temperature to cool room to
Heat temperature	Temperature to heat room to
Temperature range	Select the temperature range within which the room temperature is maintained based on cool and heat temperature above.
Fan control:

Fan on temperature	Temperature at which to turn on fan.
Fan speed increments	Temperature increments with which to increment fan speed.
Room vents control:

Rooms vents	Room vents if specified are automatically controlled with thermostat and temperature.
 


Adjacent Room Settings
Adjacent rooms allow specifying which rooms are adjacent to that room so you can automatically turn on lights in the next room when moving through this room or force adjacent rooms to Checking state when there is motion in this room.

Adjacent rooms	Select the adjacent rooms to this room.
Adjacent room motion	If motion in adjacent room force motion check in this room to confirm someone is still in this room.
Adjacent room lights	If motion in this room move adjacent rooms to Checking state so lights come on dimmed and lights the pathway.
 


Announcement Settings
Announcement settings for rooms with support for both speakers and color announcements.

Spoken announcement settings:
Specify speaker devices and timings to use for spoken announcement.

Speakers	Select speaker for spoken announcements
Speech	Select speech device for spoken announcements
Media player	Select media player for spoken announcements
Volume	Volume to use for spoken announcements
Variable volume	Use variable volume for spoken announcements
Spoken announcement during hours:

From hour	Announcements are made from this hour
To hour	Announcements are made to this hour
Color announcement settings:
Specify color bulbs and timings to use for color announcement.

Switches	Color bulbs to use for color announcements
Color announcement during hours:

From hour	Announcements are made from this hour
To hour	Announcements are made to this hour
Announcement modes:

Modes	Announcements are only made in these modes
Contact announcement settings:
Settings for door and window spoken and color announcements.

Announce door	Announce when door opens or closes
Speaker	Announce with speaker
Color	Select color for announcement
Announce stays open	Announce when door stays open every so many minutes
Speaker	Announce with speaker
Color	Select color for announcement
Window announcement:

Announce window	Announce window opens or closes
Speaker	Announce with speaker
Color	Select color for announcement
 


Mode and Other Settings
Miscellaneous settings that don't fit any where else, like in which modes should all automation be disabled or what icon to use for the room in the rooms manager and a few other settings.

Away modes	The room is set to VACANT when mode changes to any of these away modes.
Pause automation modes	When in any of these modes all automation is paused for rooms.
Days of week	Days of week which no automation should run, like say you didn't want to run any automation on Sundays.
Celsius	Set this to switch input and display from fahrenheit to celsius.
Icon URL	Icon to use for this room in Rooms Manager.
Dim lights off	When turning off lights this dims them to off over specified number of seconds instead of turning them off directly.
Turn all off	This turns off all switches when no rules match so you don't need to create a rule for Vacant state to turn off lights.
Only on state change	This processes the rules every 5 minutes on ST and every 1 minute on Hubitat to process the rules and set any matching switches .
Volume	Volume for announcements when music device is specified.
Contact announce	Announce when contact sensors open.
Contact stays open announcement	If contacts specified are outside doors this lets you select intervals in which to announce the door is open till its closed again.
Rooms_device.on()	Ability to select which state represents on() when device is turned on programmatically from webCoRE, Smart Lighting or Rules Engine.
 


View All Settings
What the name says.

 

For a github install from repo in ST use : owner: adey / name: bangali / branch: master. Install and publish the rooms occupancy DTH then install and publish the rooms manager and rooms child app smartapps. So 1 device driver and 2 smartapps ALL need to be saved and published before using the smartapp.

For a manual install contact the coder @ h20rider83@bellsouth.net, in order of DTHs and smartapps you should save and publish.

rooms occupancy DTH:

rooms child smartapp:

Then go to ST app -> Automation tab -> Add a Smartapp -> My apps in ST app and install rooms manager app then create your rooms within rooms manager.

When creating a room first give the room a name and save the room then go back in to the room to add various settings to the room. This is because the app uses app state to manage the rules and in ST the app state is not consistent till the app has been saved once.
Like the rooms app and want to contribute? Here are some options:
Like this post to help other users find this app
Submit a feature request on this thread or by creating an issue on Github
Submit a bug for something that is not working quite right here or on Github
Donate to support development of the app: donate here.
 

Non-obvious rules:
1. Outdoor lights with no motion sensor?

Setup a room say `Outdoor` with the following settings specified for the rule:
Name of the rule.
Time from and to settings when the lights should turn on and off respectively.
Lights or other switches to turn off.
Optionally you can also specify the level, color and color temperature or use a Holiday Light rule that you have setup.
The light will turn on at the time from time and turn off at the time to time. Off course you could create multiple such rules in this Outdoor room to turn off different lights at different times even on different days of the week.
2. Turn off switches after X seconds with no motion sensor? (power saver)

Setup a room with the following Engaged settings:
Set the switches you want turned off as engaged switches.
Specify the seconds after which you want the light turned off as the timeout setting.
Then add a rule with the following settings:
Name of the rule.
From the state drop down pick state as Engaged.
All switches in Engaged settings as switches to turn on.
Any of those lights when turned on will be turned off after that specified number of seconds.
3. Want to turn on/off switches on a certain day of the year?

Setup a room with the following Engaged settings:
Set all of the switches you will turn on as engaged switches.
Then add rules with the following settings:
Name of the rule.
From date and to date. (make sure hide advanced settings is false on the main settings page)
Switches to turn on.
Switches to turn off.
When the rules date condition is met, switches specified in the rule will be turned on and off respectively.
 

Here are a couple of screenshots of the device tiles for a Rooms Occupancy device from SmartThings. Note this is not applicable for Hubitat since Hubitat does not have device tiles, at least for now.

	
Finally here is a screenshot of the rooms child settings page which captures all the settings groups available for each room. On both SmartThings and Hubitat this looks quite similar except that one is thru the app interface and the other is html.


© 2020 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
