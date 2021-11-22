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


---

### Moving pol to external drive

* Step 1 : prerequisites
 Drive space: it need enough disk space to store the actual content of your ~/.PlayOnLinux directory.
 The filesystem type used for the drive should support POSIX semantics (file rights, symlinks,...) for Wine to work correctly: ext2, ext3, ext4, btrfs, reiserfs, xfs, jfs, etc. should be fine. FAT and NTFS will not work using this method.
Be sure PlayOnLinux is not running
Doing some backups at that point can't hurt
* Step 2 : moving ~/.PlayOnLinux
Move ~/.PlayOnLinux to the target filesystem, using some tool that, again, preserves all POSIX filesystem semantics. Copy then remove will give you some extra safety, so I suggest:
Use GNU's cp -a; Say you want to move PlayOnLinux's files inside /mnt/extradisk/mysecondhome/, type
$ cp -av ~/.PlayOnLinux /mnt/extradisk/mysecondhome/
(using tar, cpio, and other *nix-ish backup software should do, if you prefer using those).

* Step 3 : deleting ~/.PlayOnLinux
Once you're confident the files have been moved over, rm -rf the source directory:
$ rm -rf ~/.PlayOnLinux
* Step 4 : creating a symbolic link
Put a symlink where the source was, pointing to the new location. Example; say you moved ~/.PlayOnLinux to /mnt/extradisk/mysecondhome/.PlayOnLinux. then use
$ ln -s /mnt/extradisk/mysecondhome/.PlayOnLinux ~/.PlayOnLinux
Variants (more advanced, and not detailed here):
Move ~/.PlayOnLinux/wineprefix instead of ~/.PlayOnLinux if you prefer moving around only the virtual drives (not installed Wine versions, resource files, temporary directory, etc.).
Move specific virtual drives ~/.PlayOnLinux/wineprefix/PrefixName instead; This will give you more flexibility, but this can only be done after they've been created, and removal from PlayOnLinux may just remove the symlink, not the remote virtual drive, so keep in mind that creation and removal of virtual drives won't be fully automatic any longer if you go that path
Use mount instead of symlink. The target directory should be the root directory of a new filesystem, and instead of creating a symlink, create a directory and use it as a mount point for the new filesystem. To make it permanent, add mount instructions to /etc/fstab
(Linux only) Use mount --bind instead of mount. Target directory does not need to be the root of a filesystem, but it's otherwise similar to above instructions using mount.
Retrieved from "https://wiki.playonlinux.com/index.php?title=How_to_move_PlayOnLinux_virtual_drives_to_another_disk&oldid=989"

