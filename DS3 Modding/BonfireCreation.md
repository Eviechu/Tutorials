# How to create and delete bonfires in DS3.

1 - Know how bonfires work in Dark Souls.
2 - Get familiar with DSMapStudio
3 - Get somewhat familiar with EMEVD editors (we need to register new bonfires here. DarkScript is the editor)
4 - Get used to working with Yabber.
5 - A tiny bit of patience.

Bonfires are comprised of the following things:
1. An object (This is the "physical bonfire") -> This is what you see in the map, DSMapStudio will render it too.
2. An "enemy". -> This is the "NPC" you talk to when you rest at a bonfire. The bonfire itself is just that... an object. It does nothing. This is usually shown in DSMapStudio as a red half sphere.
3. A "Spawnpoint". -> This is where the bonfire should place you when you die and respawn. It is shown as a yellow octahedron (Just 2 pyramids glued to each other.)
4. A "Player". -> The place you warp to. It's shown as a dark yellow Hexagonal Pyramid

Before modding, make sure you unpack the game using UXM.
To do this, download UXM from the following link: [UXM](https://github.com/JKAnderson/UXM)
Once downloaded, go ahead and open it.
Click browse and navigate to your DS3 Folder `..\Steam\steamapps\common\DARK SOULS III\Game`
Click on the `DarkSoulsIII.exe`
Press `Unpack` and wait for it to finish. After this, you can close it.

Next step! Getting familiar with DSMapStudio.
You can find the download here: [DSMapStudio](https://github.com/soulsmods/DSMapStudio)
Open it up, this will be where you do 90% of your modding, give or take.
Now, press file on the top left corner and then `New Project`
Choose a name, we'll go with "New Bonfires"
Pick your project directory, this can be any folder you want, it will store the mod's files here.
Pick your DS3 Executable by browsing to your `.exe` location. Remember the UXM step? Same thing.
Click Create, you're done! Now you have a modding environment.



## Creating a bonfire!

This is where it gets a little more interesting and a teeny tiny bit more complicated.

> Before we start, I'd like to recommend that you pick a map to work on, check its ID on DSMapStudio (On the Map Editor, left panel, there are maps with names and their respective IDs. 
> For example: `m30_00_00_00` for High Wall of Lothric. We'll pick this one for this tutorial.)  

1. Navigate to your DS3 Folder once again, find the following folders: `event`, `script` and `menu`.  
2. Create 3 folders with the same name on your Mod folder. (The one you created before)  
3. Your Mod folder should now have an `event` folder, a `script` folder and a `menu` folder.  
4. Open the `script` folder and create yet another called `talk`.  
5. Open up the `script` folder on your DS3, go inside the `talk` folder and copy the file `m30_00_00_00.talkesdbnd.dcx` over to your new `talk` folder.  
6. Now, open your game's event folder. `..\Steam\steamapps\common\DARK SOULS III\Game\event`  
7. Copy `m30_00_00_00.emevd.dcx` to your Mod's `event` folder.  
8. Now, open up your Mod's menu folder and create one named `mapimage`.  
9. Navigate to your DS3 counterpart `..\Steam\steamapps\common\DARK SOULS III\Game\menu\mapimage` and copy `01.tpf.dcx` to your Mod's `mapimage` folder.  



You're now ready to start modding High Wall of Lothric.


Go back to DSMapStudio, click on Map Editor, right click on `m30_00_00_00` and click Load Map.
This is High Wall! Hold right mouse button (RMB) to control the camera, WASD (while holding RMB) to move, CTRL to slow down and SHIFT to speed up. You can control each individual speed by using your scroll wheel.  
Now, navigate to a place you know has a bonfire, for example the Tower on The Wall Bonfire.  


> NOTE: For the next parts, I'll call our Mod folder %MOD FOLDER%. Remember that this placeholder name is whatever name you picked for your own Project's mod folder that you created earlier.  
  
1. Click on the red half-sphere and note down its `Talk ID`. 
We **will** need this later.  
  
1. Hold CTRL and click on all the items mentioned above, the "Object", "Enemy", "Player" and "Spawnpoint".  
  
2. Press CTRL+D to duplicate, drag everything to the desired place (do not click anywhere else or you'll have to select all of it again).  
  
3. Once that's done, find an object nearby and see which `CollisionName` it has.  
Sometimes, objects will not have a `collisionName` and will instead use `drawGroups`, you can still use these by copying them directly or (while having the object selected), going to the Render Groups tab on the bottom of the screen, clicking `Get DrawGroups` then navigating to your new object and clicking `Give as DrawGroups`.  
  
4. Copy it to every item we just dragged (not all of it needs a `CollisionName`, if the field doesn't exist then just ignore it). 
This will tell the game to render it when we're on top of that collision.
  
5. Now we take care of the ID fields.
   1. Select an unused Entity ID for the "Enemy". As an example we'll go with 3000900. Again, this is the **Enemy's** Entity ID.  
   2. Click on the "Object" and give it an ID that's equal to the `Enemy's ID + 1000`. So in our case, 3001900.  
   3. Click on the "Spawnpoint" and give it an ID that's equal to the `Object's ID + 1000`, in our case, 3002900.  
   4. Click on the "Player" and give it an ID equal to the `Enemy's ID + 20`. In our case it would be 3000920.  
  
1. After you've completed the step above, open up your map's `emevd.dcx` with DarkScript. (Reminder, it's on `%MOD FOLDER%\event\m30_00_00_00.emevd.dcx`)  
Search for the line "RegisterBonfire" (again, CTRL+F is your friend) and look at the first number inside the parenthesis.  
Note down the highest one and search for the next one (So if our number is 13010000, we search for 13010001), if DarkScript doesn't find anything, we're good! Memorize that number.  
  
1. Add a new line below or above them and write `RegisterBonfire(13010001, 3000900, 5, 180, 0);`  
Save the file and exit DarkScript.  
> Explanation: First number is the EventID, we just need to give it an unused number. Second number is your "Enemy" Entity ID. Third number is the distance at which the player can use the bonfire. Fourth number is the angle at which the player can use the bonfire. And the last number is the standard Kindling level of the bonfire.  
  
1. Open up your talk script folder, this is located under `DARK SOULS III\Game\script\talk`. Unpack your map's `talkesdbnd.dcx` file.  
[Drag `DARK SOULS III\Game\script\talk\m30_00_00_00.talkesdbnd.dcx` on top of Yabber.exe]  
  
1. Then, keep opening the folders until you see a bunch of ESD files. Find the one with the number you wrote down in step 1. [The **Talk ID**]  
Duplicate that one and give it a new name, simply change the last number to whatever the next one is, as long as it isn't used.  
[For example, if our number is 300000 then we need to name it `t300001.esd` if that's taken, pick the next one. So on and so forth.]  
  
1. Go back until you find your `_yabber-bnd4.xml`. Open it with any text editor and copy any entry.  
Copy from one `<file>` to the next `</file>` and paste it at the end.  
Rename the ID inside of it to the next unused one.  
So if the last is 119, we name it 120.  
  
1. Change this row `<path>script\talk\m30_00_00_00\t300000.esd</path>` to your Talk ID, remember that we picked one before.  
In our case it's `t300001.esd` so rename it to `<path>script\talk\m30_00_00_00\t300001.esd</path>`.  
Go back again until you can see your `m30_00_00_00-talkesdbnd-dcx` folder and drag it on top of Yabber.exe.  
  
1. To create an entry on the Bonfire Warp menu we need to delve into the Params and Msg, so open up the Params Tab on DSMapStudio, find `BonfireWarpParam` and click on it.  
   1. Find a bonfire on the map you want and click on its entry. CTRL+D to duplicate, rename it to whatever you want.  
   2. Change `LocationEventId` to the next unused number, so if the one you copied is `13000004` then type `13000005` on this field. Then, on the `WarpEventId` field, write the Entity ID of our "Enemy". So in our case, 3000900.  
   3. Now open up DSMapStudio's Text Editor and find the `MenuText` entry on the left panel.  
      1. Search for the name of a bonfire near the place you want, so if our map is High Wall of Lothric then we can search for Vordt for example.  
      2. Find an unused ID near this bonfire and rename it to whatever you want. We'll go with "Test Bonfire". Note down the ID. 
      3. Go back to the Param Tab and add that same ID to the `BonfireNameId` field.  
      4. On the next field `DescriptionTextId` we add an ID equal to `BonfireNameId + 400`, so if our ID was 211200 then our new one is 211600.
  
1. To add a picture to our bonfire, we need to take one (or pick any picture for learning purposes) of the area your bonfire is at and save it somewhere easily accessible. We'll need this for `Picture ID`, which gives us a pretty image on our warp menu. Then, we proceed as follows:
   1. Open up your `DARK SOULS III\Game\menu\mapimage` folder and find the `.tpf.dcx` file corresponding to your map. For example, 01 is High Wall of Lothric and 02 is Foot of The High Wall.  
   2. Drag it on top of Yabber.  
   3. Open the newly created folder and open any image that's inside with Paint.NET (I recommend this one. If you're on Linux then Gimp is fine.)  
   4. Add your picture on top of this one by dragging from its location to the Paint.NET window. Click `File` on the top left corner, `Save as...` and pick DDS as the format.
   5. As for the name, copy one of the other names in this folder. In our case if the last one is `MENU_MapImage_10025.dds` we save it as `MENU_MapImage_10026.dds`. DXT1 is fine (this is the default, just press save)  
  
1. Open up `_yabber-tpf.xml`. You should know what to do by now. 
Find the last entry, copy everything from the first `<file>` to the last `</file>` and paste it at the end.  
After this, change the Name row from `<name>MENU_MapImage_10025.dds</name>` to `<name>MENU_MapImage_10026.dds</name>`.  
Save it, go back and drop the folder onto Yabber.exe. You now have a custom picture!  
  
1. Go back to your Params, find the PictureID field. Paste the ID we chose in here. In our case, 10026.  
    1. ListID tells the game where to put it in the menu. 1 is for High Wall of Lothric (same as the file we opened before).  
    2. `IsDisableQuickwarp` is better left unchecked, this is for Firelink Shrine only.  
    3. `CeremonyID` is fine left at -1 and `OnlineAreaID` is fine left as is. (If you copied one from the same area, otherwise just find it and copy from another bonfire nearby.)  
    4. Save everything. You should be done!
  
  
## To delete a bonfire:  
  
  
Easy, either delete everything from the map or, if you wish to be clean about it... Open up DarkScript and open your map's emevd file. 
This is located at `DARK SOULS III\Game\Event\m30_00_00_00.emevd.dcx`. 
  
**vvv       Beyond this point, everything is mostly unnecessary       vvv**  
  
1. The file name varies based on what map you want to change. Memorize which one it is.  
   
2. Go look at your bonfire's "enemy" and note down the EntityID. CTRL+F and paste the following in there `RegisterBonfire`. Press Enter and look for your ID, should be something like 3000950 (this is an example).  
   
3. Comment it out by adding `\\` before that line or simply delete it.  
   
4. Open up `DARK SOULS III\script\talk\m30_00_00_00.talkesdbnd.dcx` (again, the name changes based on your map) with Yabber by dragging the file on top of Yabber.exe.  
   1. Open every folder until you reach a bunch of `ESD` files.  
   2. Delete the one for your bonfire, the exact number can be known by clicking the "Enemy" on DSMapStudio and finding the "Talk ID" entry on the right panel.  
   3. Go back until you find the folder named `script` and a file named something like `_yabber-bnd4.xml`.  
   4. Open this file, find your "Talk ID" (Press CTRL+F and write your number here.)  
   5. Delete everything from the first `<file>` before your ID to the first `</file>` after your ID.  
   6. Go back once until you see your `m30_00_00_00-talkesdbnd-dcx` folder. Drag the folder on top of Yabber.exe
   7. You're done and should now see a `m30_00_00_00.talkesdbnd.dcx.bak`. This is the automatic Backup file Yabber creates. It means your file was successfully replaced.

