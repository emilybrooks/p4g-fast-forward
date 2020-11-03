# Enabling Music During Fast Forward in Persona 4 Golden (Steam)

## Step 1: Music during fast forward

Make a backup of `Persona 4 Golden\P4G.exe`

Open P4G.exe in a hex editor

### For version 1.0 of the exe (released 6/13/2020)

At offset 0x63D9B4E, highlight:

```F3 0F 11 0C B5 B8 4B E9 05```

Overwrite with:

```90 90 90 90 90 90 90 90 90```

### For version 1.1 (released 9/1/2020)

At offset 0x42CFEE, highlight:

```F3 0 F11 0C B5 B8 1B E6 05```

Overwrite with:

```90 90 90 90 90 90 90 90 90```

Note: There's a few quirks with this. A small amount of the voice lines will still play during fast forward, and some of the background music (for example, junes) is on the same channel as the voices so it remains muted.

## Step 2: Replacing the VCR sound with silence

Make a backup of `Persona 4 Golden\SND\BGM.xwb`

### Install .NET Runtime 3.1.5
https://dotnet.microsoft.com/download/dotnet-core/3.1
The file you want is Desktop Runtime 3.1.5, probably x64 if you have a modern cpu


### Download XactTool
https://amicitia.github.io/post/xacttool

Note: As far as I know this program is only hosted as a discord upload. If this link stops working let me know.

### Edit SND.xwb

Note: Replace the file paths to correspond with where your game is installed and where silence.wav is located.

Replace SYS_REW.wav
```
xacttool -wb "F:\Steam\steamapps\common\Persona 4 Golden\SND\BGM.xwb" -r "F:\Downloads\silence.wav" -i 1050
```

Replace SYS_STOP.wav
```
xacttool -wb "F:\Steam\steamapps\common\Persona 4 Golden\SND\BGM.xwb" -r "F:\Downloads\silence.wav" -i 1051
```

## Step 3: Removing the scrolling static

### Extracting the PAC file
Download NR2_unpacker https://modworkshop.net/mod/17641

Note: The texture we're trying to replace is in multiple pac archives, and only one gets loaded depending on which language the game is running in. I'm working with the assumption that you want to modify the english version, which will be data00004. I believe japanese is data00001, and data00005/data00006 are for some other languages I haven't confirmed.

Make a backup of `Persona 4 Golden\data00004.pac`

Drag data00004.pac onto nr2_unpacker.exe

There should now be a data00004 folder in your game's install directory

### Modifying init_free.bin
Download Amicitia
https://github.com/TGEnigma/Amicitia/releases

Open `Persona 4 Golden\data00004\init_free.bin` with amicitia

Open the tabs for init/camp.arc > event_skip.spr > textures

Right click noiz, replace with noiz.png
Right click noi, replace with noi.png

File > save to save the modified init_free.bin

### Editing the PAC file

Download Pac Editor
https://github.com/MysteryDash/Dash.FileFormats/blob/master/Tools.zip

In pac editor, drag data00004.pac

Drag in your modified init_free.bin

Save the pac (you'll have to name it something else or the program won't succeed)

Rename your modified pac to data00004.pac
