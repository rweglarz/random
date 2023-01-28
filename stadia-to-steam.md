How I moved Cyberpunk 2077 save game from Stadia to Steam / GeForce NOW
===

As I couldn't find a step by step doc describing the process I decided to note it down.

> **Warning**
> I'm not responsible for any save game you might lose by repeating the process

Process worked for me, does not mean it will work for you. I had no save games on steam for any game

My intention is to play via GeForce NOW, at least for now. I started the game in it once before attempting this process.


# Requirements
* Stadia save game export / takeout
* Steam Client on linux


# Process

## Cyberpunk on linux
Download/install Cyberpunk from steam. In properties of the game enable compatability mode "Force the use of specific Steam Play compatability" tool.
Launch the game. For me, probably due to poor graphics card it does not even start but that seems to not be necessary. 

## Cyberpunk save game
I installed the steam client via snap hence my save game folder was:
```
~/snap/steam/common/.local/share/Steam/steamapps/compatdata/1091500/pfx/drive_c/users/steamuser/Saved Games/CD Projekt Red/Cyberpunk 2077
```
In this folder I only had this files/folders:
```
> ls -1
AutoSave-0
steam_autocloud.vdf
user.gls
```

### Stadia save games
Save games from stadia, after unpacking landed in:
```
~/Downloads/stadia-takeout-2023-01-18/takeout-20230118T212812Z-001/Takeout/Stadia/GAMING/GAME_SAVE
```
Among all the files the intersting one was the newest save:
```
Cyberpunk 2077_1047_gamesave.zip
```
with the following content:
```
> unzip -l Cyberpunk\ 2077_1047_gamesave.zip
Archive:  Cyberpunk 2077_1047_gamesave.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
   214318  01-06-2023 10:16   screenshot.png
  6709159  01-06-2023 10:16   sav.dat
     5897  01-06-2023 10:16   metadata.9.json
---------                     -------
  6929374                     3 files
```
which had exact same files as the autosave-0 folder in the steam folder:
```
> ls -1 AutoSave-0
metadata.9.json
sav.dat
screenshot.png
```

### Prepare the save game files
unzip the save game:
```
mkdir ttt
> unzip Cyberpunk\ 2077_1047_gamesave.zip -d ttt
```
I don't know if it matters but to be on the safe side, check the save game name:
```
> grep name ttt/metadata.9.json
            "name": "ManualSave-15",
```

## Create Steam save game
In the stadia save game folder create the folder and copy the files:
```
mkdir ManualSave-15
cp ~/Downloads/stadia-takeout-2023-01-18/takeout-20230118T212812Z-001/Takeout/Stadia/GAMING/GAME_SAVE/ttt/* ./ManualSave-15/ 
```

## Start the game
For me it of course silently failed again but it seemed to have triggered the save game sync.
I navigated to: https://store.steampowered.com/account/remotestorage -> Cyberpunk / "Show files" and the file was there.
![steam save game files](https://github.com/rweglarz/random/blob/media/images/steam-saves.webp)
After starting the game in GeForce Now I got an error about save games not being able to sync but luckily it sounded more like a warning and I could actually load the new save game.
