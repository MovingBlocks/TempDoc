Key Bindings
===============================

The following are the basic keys enabled in Terasology for you to interact with the world. There are additional keys with [[Debug Features]] enabled

* [W,A,S,D] - Movement
* [E] - Activate (Chest, TNT, etc)
* [Q] - Throw held (block) item (hold down to charge for a longer throw!)
* [Space] - Jump
* [Double Space] - God mode (fly / no-clip)
* [Shift] - Hold to run
* [Left click] - Activate left click action (default = place block)
* [Right click] - Activate right click action (default = remove block)
* [Mouse wheel up/down] - Cycle through toolbar slots
* [1..0] - Change the active toolbar slot
* [I] - Toggle inventory screen
* [H] - Hide user interface
* [F] - Toggle viewing distance (near, moderate, far, ultra)
* [Tab] - Toggle developer console
* [Escape] - Show/hide the game menu screen
* [F3] - Toggle debug mode and information
* [F4] - Different debug metrics
* [F5] - Show block picker GUI element

Debug Features
----------

These keys are only active if the player first uses `F3` to enter debug mode

* [Arrow up/down] - Adjust the current time in small steps
* [P] - Activate first-person player camera
* [O] - Activate animated spawning point camera
* [K] - Kills the player

Inventory
----------

There are a fair bit of nice shortcuts that work in the inventory

* Using the mousewheel over an item stack will add/remove items from it
    * Left-CTRL will do so at double speed (2 items at a time)
* Shift-clicking on an item will insta-move it from one side to another in a transfer (like inventory to chest) - or should that be made CTRL instead?
* Right-clicking an item stack will pick up half of it (or drop a single item if used with a stack held over an empty or compatible stack)

Other keyboard layouts
----------

There are two commands available in the commandline to change the keybindings. The supported keyboard layouts are AZERTY and NEO 2 layout.

* Use /AZERTY to set the bindings fitting the azerty layout:
   * Z : forward
   * S : back
   * Q : left
* Use /NEO to set the bindings to fit the neo 2 layout:
   * V,I,U,A : moving
   * L : use item
   * G : inventory