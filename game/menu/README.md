# Information for Contributers

## GameManager
The GameManager keeps track of all minigames and starts/stops them when needed.  
It also has a rudimentary game selection menu that uses the GameDisplays.  

## GameDisplay
Is used my the GameManagers game menu to show what the game is about.  
It has a button to load the game & a popup for more detailed infos but no logic beyond that.  

## PauseMenu
The PauseMenu is autoloaded like GameManager. It will pause the game using `get_tree().paused`.  
It uses `_input()` as a trigger so it won't interfere with other UI or gameplay.

# API
## GameManager

* **`load_game(game_cfg: ConfigFile)`**  
  Loads the game specified by the config file.

* **`end_game(message:String="", _status=null)`**  
  Ends the game and displays `message`. This behaviour will change in the future.  
  `_status` isn't used at the moment. It is meant for the score the player achived.  

* **`_build_menu()`**  
  Creates a menu using GameDisplays for the cached `game.cfg` files in `_games`  

* **`_find_games()`**   
  Searches every folder inside "res://games/" for files called `game.cfg` and caches them in `_games` using `_load_game_cfg_file()`.  
  `_games` is cleared at the start.  

* **`_load_game_cfg_file(path: String)`**  
    Loads any config file into `_games`.  
    Any valid .cfg will be loaded. There are no checks to prevent incorect data from loading.  

## GameDisplay
* signal **`pressed(game_file)`**  
    Is emitted when any load buttons of the display are pressed.  
    `game_file` is the config used when setup was called.  

* **`setup(game_cfg: ConfigFile)`**  
    Loads the data from the given `game.cfg` into the correct labels.  

## PauseMenu
* signal **`pause_menu_opened`**  
  emitted when the menu opens but before `get_tree().paused` is changed.
* signal **`pause_menu_closed`**
  emitted when the menu closes but before `get_tree().paused` is changed.
* **`show()`**  
  Shows the pause menu. Use this to open the menu from code.
* **`hide()`**  
  Hides the pause menu. Use this to close the menu from code.
* **`is_open()`**  
  Returns `true` if the menu is open.
* **`_update_menu()`**  
  Private function to configure the buttons when the menu is shown.
