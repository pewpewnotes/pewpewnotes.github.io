```

  ____                 _             
 / ___| __ _ _ __ ___ (_)_ __   __ _ 
| |  _ / _` | '_ ` _ \| | '_ \ / _` |
| |_| | (_| | | | | | | | | | | (_| |
 \____|\__,_|_| |_| |_|_|_| |_|\__, |
                               |___/ 
```

### Gaming with Lutris

---

Start lutris and then click on second icon from left at top of the window “Manage Runners”. 
Scroll down to wine and select “Manage Versions” Lots of versions pop up, you can install whatever one you like, although ge3.6 is a great base for many games. 
NB.
you don’t have to do this every game, this is just grabbing the bottles for future use.
Now click on the + “Manually add a game” icon. 
In the first window “Game Info” give the game a name (can be anything).
Choose “Wine” as a runner from the pull down.
In the second tab “Game options” locate your installer from gog or wherever you got it from and select it as your “Executable” (we will change this later. 
Ignore arguments and working directory unless you need to put stuff in there specific to your game. “Wine Prefix” I choose /Games/fallout for example, and generallly select 64bit for prefix architecture. 
Under “Runner options” you can choose different wine versions for your bottle.
This can be changed at any time to update to a new or different version. 
Ignore “System options” you can come in here later if you need to.
“Save” and it will exit. 
if you don’t see you game in the list in Lutris, restart as there is a minor bug that won’t show launch banners until you have at least “one game” installed.

Ok now you run your game and it should start up your installer, install the game as you would in windows and it will automatically be pushed into the prefix you selected earlier.

Once all of that is done, last little bit. Right click your game banner in the Lutris main screen and select “Configure”, go to the “Game Options” tab and change the “Executable” to point to the actual .exe of the game you installed instead of the installer.
It will probably be in /Games/your prefix/Drive_c/program files (X86) directory somewhere. Now just “Save” and give your game a try.

Hope this helps.

Quick addendum regarding DXVK. To install DXVK to the bottle/prefix you have created, when you are in “Runner options” simply tick the enable DXVK box. Don’t select any DXVK version, instead simply type “0,54” in the version pulldown box and it will download and install 0.54 directly to your prefix.
Oh and I have found that wine 3.9 firerat is probably your best version for getting many games to run at this time.
