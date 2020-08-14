# PendEdit - Pendelum Level Creation Tool

The following documentation will provide a quick overview over the usage of the [PendEdit](https://pendedit.pendulumgame.com/) Level Creation Tool for [Pendelum](https://pendulumgame.com/).

Of course the game contains a level editor by itself, but if you want to have more controls and features concerning the level creation flow, PendEdit will provide a much richer experience in creating levels.

**Please note that a copy of Pendelum as well as authorization is required for PendEdit to work!**


# Getting Started

## Installation

Download the installer *.exe* file and execute it. Due to Windows safety mechanisms it is most likely that Windows will block the installer from running, so you will need to confirm that you want to run it anyhow.
**Why is this?** Well - Windows does not like unsigned software and wants developers to own a Authenticode License which currently costs around 300$ per year. I personally do not think that it is worth spending that money on a tool that i mainly created for myself, so i didn't take the effort to buy one - deal with it. :P
If you still feel uncomfortable executing the installer, you can run a bunch of antivirus checks on the .exe or just don't install it. It's okay.

> This can change in the future - maybe one day the installer will be signed and this section will be removed completely. But until then, it is a matter of fact.


## Authentication

For PendEdit to work for you, two requirements must be met:
1. You need to own a valid copy of *Pendelum* on Steam
2. You need to be registered as a PendEdit Creator

To apply for a PendEdit Creator registration please write an email to support@pendulumgame.com containing your name and your SteamID. Please avoid submitting an application only containing these two things, a full text is always nicer to read.

## Starting PendEdit
To get into the editor, you need Pendelum running in MapHook mode. You can practically close the game once the editor is running, but I recommend not to do so due to level testing purposes.

### Updates
Once PendEdit is installed, no further manual download is required. The app will check for updates or update itself every time it is loaded up.

## MapHook mode
Pendelum is capable of receiving level data on the fly to test ingame due to a game mechanic called *MapHook*.
MapHook connects to PendEdit once activated and listens for level data to transform into a regular playable map.

To enter MapHook mode, open the ingame console by pressing `Page Up` and execute the command `maphook enable`.
Pendelum should automatically abort any ongoing ingame action and enter MapHook mode.

To disable MapHook either restart your game or execute the console command `maphook disable`

# Using PendEdit

PendEdit was designed to be as user friendly but efficient and powerful as it can possibly be, but nevertheless there are a few things to explain.

## Navigation Bar
The Navigation Bar is the "app control center" and it should not take any more explanation to understand it. Anyways, here is a quick overview:

### File Control Area
There are 3 options:
- **New** lets you clear the current editing map buffer and start from scratch with an empty scene
- **Open** lets you load an existing map file into PendEdit. The preferred file type is the Pendelum Map File extension *.pndx*, but the editor also accepts *.bytes* as a format.
- **Save** lets you... ah god dammit - you know what a save button does!

> **NOTICE:** If you want to open files created with the ingame editor, you can find these in the LocalLow folder at `%UserProfile%/AppData/LocalLow/thelaumix productions/Pendelum/e.<HEX-SteamID>`

> **WARNING** It is not recommended to rename any files and folders, including map names or creating your own map names for the ingame editor maps. Please do not try to create your own mapfile names as this can lead to runtime issues or level handling errors.
> The best way of bringing PendEdit files into the editor is to create a small map file with the ingame editor, open this file with PendEdit and save it as the exact same file.

### Play Mode
The big *Play*-Button will set PendEdit into Play Mode. Again, you need to have Pendelum running in the background with MapHook mode enabled for the level data transmission progress to succeed.
Once the level has ended either by reaching the goal or aborting the game, PendEdit will return to Edit Mode.


## Element Controls

The bottom part of the UI holds the Element Controls. They consist of the selector buttons for MapElement types showing the current count of respective elements the current map is holding and the overall map meta data.

You can either click the buttons to select the respective element or hold `Alt` followed by the element number *(counted from left to right and top to bottom)*

### Map Meta Data
|Meta Name| Purpose |
|--|--|
| Channels | The current amount of actively used channels.<br>Actively used means that every input or output on each channel set must be linked successfully |
| Elements L0 | The total element count on the main layer |
| Elements L1 | The total element count on the background layer |
| Elements L2 | The total element count on the foreground layer |
| File Size | The amount of Bytes the final map file will be once saved * |

> **Please keep in mind that the upload limit for community maps is 5KB*

## Element Types

> This table uses logic signal types. For more information on logic signals read section below

|Element| Description |
|--|--|
| **Block**<br>**Ramp**<br>**Rampicle Concave**<br>**Rampicle Convex**<br>**Ramp Forward**<br>**Ramp Backward**<br>**Pillar Base**<br>**Pillar Center**<br>**Window** | Decorative or fundamental elements. No logic |
| **Cam Anchor** | Defines the camera distance from the pendulum. Works by distance detection: The closest anchor will be taken as distance parameter. |
| **Spawner** | Spawns a pendule. Can be set to default, red or blue.<br>Two spawners of the same type can be set, but the game will most likely throw up problems if you do so. |
| **Goal** | The goal to throw the pendule into. Can be set to default, red or blue. |
| **Button** | Logic: Button. Toggles on collision. Sends `ON` / `OFF` signals. Can spawn disabled or enabled.|
|**CO: Synchronous Button**| Logic: Button for Co-Op purposes. Must be exactly 1x red and 1xblue on one channel to work correctly. |
| **Photo Sensor**| Logic: Sends an `ON` signal once a pendule passes through. Can be re-enabled by an `iOff`. Detects its length automatically. |
| **Timer**| Logic: Starts a specific timer on receiving an `ON` signal. Sends `ON` to its output channel once activates. Once disabled either by an external `OFF` signal or because the timer ended, the timer will stop and send `OFF` to its output channel.<br>Minimum time is 500ms. Can be set in steps of 0.5s |
| **Relay**| Logic: Used to delay or invert incoming signals and relay them to its output channel. When inverting, incoming `ON` signals will be relayed as `OFF` signals and vice versa. <br>Delay can be set in steps of 100ms. |
|**Barrier**| Logic: A "force field" style barrier that blocks passage once enabled. Can spawn disabled or enabled. Toggles state on `iOn` / `iOff` inputs. Detects its length automatically. |
|**Door**| Logic: A trap door that blocks passage. Can spawn open or closed. Toggles state on `iOn` / `iOff` inputs. |
|**Wind Machine**| Logic: Applies wind-like force to a pendule in front of it. Strength depends on distance and can be changed. Can spawn disabled or enabled. Toggles state on `iOn` / `iOff` inputs. |
|**Trampoline Straight**<b>**Trampoline Diagonal**| Applies instant force on colliding pendule. Strength can be changed. |
|**Gravity Field**| Modifies the gravity of any pendules inside. Direction can be changed |
|**CO: Player Filter**| Co-Op purposes. Only lets players of specified color pass through. Detects its length automatically. |

## Logic Signals
Basically the logic in Pendelum maps consists of `ON` and `OFF` signals. But the effect on the receiver element can vary concidering the spawning state.

|Signal type| Description |
|--|--|
| `ON` *(out/in)* | Default enable signal |
| `OFF` *(out/in)* | Default disable signal |
| `iOn` *(in)* | Start-condition based `ON` input signal processing. If i.e. a door is open by default, `ON` will close it. If the door is closed by default, `ON` will open it. |
| `iOff` *(in)* | Start-condition based `OFF` input signal processing. If i.e. a door is open by default, `OFF` will return it to the initial open state and vice versa. |

> **NOTICE**: Elements sending signals won't receive the sent signals themselves

## Toolbar
The Toolbar can also be concidered as the master control panel. PendEdit uses *"Tools"* to control the workflow, each serving a different purpose in level editing.

> *Italic entries* are tools that are not listed in the floating bar UI. They can be used by key command only.

|Tool|Shortcut|Description|
|--|--|--|
|Selection|`W`| The main tool. Use to select one or multiple elements on the map canvas.<br>`Click` to select single object<br>`Shift` + `Click` to add or remove objects to or from the selection<br>`Drag` to select a region<br>`Shift` + `Drag` to select a region across all layers **(!!!)**<br><br>*If one or multiple elements are selected the **Inspector** will show up in selection mode* |
|Move|`W`| Moves the current selection.<br>`Click` + `Drag` on a selected element to move the selection around |
|Rotate|`E`| Rotate the current selection.<br>`Click` + `Drag` on a selected element to rotate all elements<br>`Shift` + `Click` + `Drag` on a selected element to rotate the entire selection matrix |
|Add|`A`|Adds a single element to the map<br>`Click` to add the element selected in the Element Controls<br>`Right Click` to change rotation|
|Remove|`X`|Removes a single element to the map<br>`Click` to remove
|Element Brush|`B`|Adds multiple elements to the map. Similar to *Add*<br>`Click` + `Drag` to draw elements|
|Eraser|`C`|Removes elements like the *Element Brush* adds them **(!!!)**<br>`Click` + `Drag` to erase elements<br>`Shift` + `Click` + `Drag` to erase across all layers **(!!!)**|
|*Duplicator*|`Ctrl` + `D`|Duplicates the selection. Once the duplicate is pasted, the selection will be updated to the new elements.<br>`Click` to paste duplicate at the preview position. **This will not check for overlaps**<br>`Esc` or switch to any other tool to cancel duplication<br><br>***NOTICE**: You can duplicate to different layers by changing the layer while duplicating. This only will work if the selection you are duplicating is non cross-layer*|
|*Flipper*| `<Ctrl>` + `<Shift>` + `F` | Flips the current selection horizontally or vertically<br>`Ctrl` + `F` to flip horizontally<br>`Ctrl` + `Shift` + `F` to flip vertically |


## Layers

A Pendelum map consists of 3 different layers:
|Layer|Id|Purpose|
|--|--|--|
|Central|`L0`| The layer where the magic happens. Usually a Pendelum game and all the logic is running on this layer. |
|Background|`L1`| Usually used for decoration and depth |
|Foreground|`L2`| Usually used for decoration and to obscure the view |

The layer purposes are for consistency, but in therory, every layer can contain logic, spawners etc.

You can change the layer by either clicking on the layer buttons in the top right corner or using the layer key commands:
- `Tab` moves one layer up
- `Shift` + `Tab` moves one layer down

## Inspector
The Inspector appears in selection mode when one or more elements are selected. It displays the type of the current selected object *(except when multiple types are selected)* and the element specific properties or controls.

Multiple elements have different properties, but some elements share them. If multiple types are selected, only properties shared between all selected types are displayed.

Usually the inspector will show the current property values. If multiple elements are selected and their property values match, the value will be displayed. In case the values don't match, nothing will be displayed until you change the value which will update the respective property on all selected elements to the specific value.

Numeric values always can be changed by hovering over the slider or input field and using the scroll wheel.


## Map Canvas
The Map Canvas is the heart of PendEdit. It contains every element the map is holding along with some Gizmos to indicate the logic and game flow.

### Navigating the Canvas
Simply use the scroll wheel to zoom in and out. To move the canvas around, click and hold the middle mouse button and drag the canvas.

### Logic Indicators
To visualize the map logic, each canvas layer holds individual logic visualizers. Those can either be:
- **Channel Connectors**: Yellow lines are drawn from each element transfering data to another on a specific channel. This can help to create complicated logic or keep an eye on logic processes. Connectors are drawn from an output to all relating inputs.
- **Status Indicators** Elements that can spawn with various states show a small dot blinking. Red means "disabled" by default, green means "enabled" by default. *(Doors are "disabled" when they are closed, barriers are "enabled" when they are closed)*

### Pendule Trails
After exiting Play Mode, the game will submit pendule trails like the ingame editor does. These trails serve to indicate the recent pendule flow inside the map.
Unlike the ingame editor which records the last 12 seconds with 5tps, the MapHook submits trails of the last 20 seconds with 10tps.

You can disable or enable pendule trails by pressing the `Home` key.
