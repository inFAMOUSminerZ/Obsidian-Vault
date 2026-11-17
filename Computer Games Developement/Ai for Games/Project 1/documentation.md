## Code

### GlobalBoard
The GlobalBoard (`global_board.gd`) is a script separate from everything that just contains
a huge pile of variables. These variables can be read and written to
from any other script by refencing it like a class:

`GlobalBoard.[variableName]`

The GlobalBoard is super useful for connecting AI features to the player.
Examples:

```GDscript
#Swordsman script
if global_position.distance_to(player_pos) < GlobalBoard.playerSafeDistance:
	GlobalBoard.playerSafe = true
else:
	GlobalBoard.playerSafe = false
```

```GDscript
#pickup generator script
func _process(delta: float) -> void:
	if GlobalBoard.recentPickUp == true:
		if GlobalBoard.i < recentWeaponChangeTime:
			GlobalBoard.i += 1
		if GlobalBoard.i >= recentWeaponChangeTime:
			GlobalBoard.i = 0
			GlobalBoard.recentPickUp = false
	if $spawnTimer.time_left == 0 and !GlobalBoard.recentPickUp and GlobalBoard.playerSafe:
		add_child(sPickup)
```

### Script Globals
Any script can be made into a global script through the project settings.
However, some of these can cause big issues for the game.
Mainly, changing the player script / `movement.gd` to a global, duplicates
the player in the scene during runtime.
Also, changing the arena / `the_arena.gd` to a global script causes the
whole scene to accelerate past the bounds of collision checks.
Why does this happen? I do not know.
Some scripts other than `global_board.gd` that function correctly as global
scripts. these being; `bow_pickup.gd`, `mace_pickup.gd`, and `sword_pickup.gd`.

Example of these in use:

```GDscript
if MacePickup.macePickedUp:
	$activeWeapon/mace.visible = true
	$activeWeapon/bow.visible = false
	$activeWeapon/sword.visible = false
if  SwordPickup.swordPickedUp:
	$activeWeapon/sword.visible = true
	$activeWeapon/bow.visible = false
	$activeWeapon/mace.visible = false
if BowPickup.bowPickedUp:
	$activeWeapon/bow.visible = true
	$activeWeapon/mace.visible = false
	$activeWeapon/sword.visible = false
```

### Health System
The way the health system works in the game is by setting up the following on the player end is that we create a function called `take_damage`, which has a parameter called `amount` which is an int equal to 1.

```GDscript
func take_damage(amount: int = 1) -> void:
```

Then we put the following at the top near the rest of the variables `var health = 4`.

Next we create a variable which is equal to an argument where we use the method "max()" which selects the highest number in a set and returns it. in the following case;'

```GDscript
health = max(health - amount, 0)
```

This means that health (which has been set at 4) is = the sum of 4 - 1 with a minimum of 0. This is so we don't have to account for further negative numbers. Then it select the highest number being 3. This is the first time the function is called of course. 

Next we use a simple if statement that checks if health is the same value as 0 and is of type int and `print("player died")`.

```GDscript
if health == 0:
	print("player died")
```

Now we have the number 3. Then we call the next function, `update_hearts()`.

To update the hearts we need to use a for loop here we loop once per heart (size being 4, so 4 times). "place" is 0 on the first pass, 1 on the next, and so on. Essentially "loop for as long as place can fit into hearts array size while being incremented".

```GDscript
func update_hearts() -> void:
	for place in hearts.size():
```

So here as you can see we say "for however many time 0 fits into the number of hearts while being incremented" do X. What we then have it do is use place to turn the heart invisible. We take whatever place is and pass it into the array we want to access like so;

```GDscript
hearts[place].visible = place < health
```

As you can see we access the visibility of a certain heart in the hearts array by using the for loop variable "place" so that every time it runs through it checks if place is less than health and if it is not then the visibility of that heart is false.

---
## Documenting

### Flowcharts
Use [Draw.io](https://app.diagrams.net/) to make a flowchart.
The syntax for a flowchart is as such:
- circle/rounded rectangle:
	start/end nodes
- rectangle:
	a process (i.e. print, write, function call, etc..)
- rectangle with bars on each side:
	I/O (input/output) node (e.g. Input.is_action_pressed())
- diamond:
	question/condition (e.g. if statements)
	arrows go to left (or just the side) for false/no, and down 
	for true/yes
	label yes/no on arrows
- irregular hexagon:
	[loops][]
- triangle:
	merge (branches)
- cylinder:
	database

### Writing documentation
when writing documentation, try to use as simple language as possible,
make it readable in multiple editors,
(some don't have text wrapping (e.g. Godot editor, KDE Kate))
go into as much detail as you can. The docs are a backup to in-line
or in script comments. Comments are still a huge part in understanding
code while the docs act as a backup and re-enforce your own understanding
of the code.

---
## Features
#### Weapon Pickups
the weapon pickup system works off of 2 combined scenes. `[weapon]Pickup.tscn` and `[weapon].tscn`.
The pickup scene has a detection radius using `area2D` which sends a signal to the 
[global] (https://www.tomen.games/progects/documentation/godot_globals) script `[weapon]_pickup.gd`
changing the variable `[weapon]Pickup.[weapon]PickedUp` to true.
This is then read by the player/`movement.gd` script which changes the visible weapon accordingly.

##### Pickup Time Passed
after picking up a weapon, a global variable on the GlobalVariable board,
`recentPickup`, is changed to true. This is to furfil the `if: time elapsed`
condition for the system.

``` GDscript
if GlobalBoard.recentPickUp == true:
	if GlobalBoard.i < 400:
		GlobalBoard.i += 1
	if GlobalBoard.i >= 400:
		GlobalBoard.i = 0
		GlobalBoard.recentPickUp = false
```

---
#### Animation Turning
The player sprite turns based on the directional key being pressed at the current time.
To do this, it reads the 2D Vector output of `direction`:

`var direction := Input.get_vector("left", "right", "forward", "backward")`

then, using a switch case in the `movement.gd` script, it selects one of four animation sets.
(left, right, forward, backwards) / (leftWalk, rightWWalk, backWalk, default)

The animation sets were added via an animatedSprite2D node.
Each one is labelled as a new animation imported from an animation sheet with
the settings: 1 vertical, 4 horizontal, frames: (0 - 3).

---
