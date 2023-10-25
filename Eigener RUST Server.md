---
tags: gamez
---

## Prerequisites

Download steamcmd.zip, entpacken in C:\steamcmd
Drinnen ist steamcmd.exe --> ausführen
Macht Updates, endet mit Steam Prompt:
`Steam>`

## Installing the Rust Dedicated Server

Run the following commands, one at a time, at the Steam> prompt, to start downloading the server to your computer.

```
Steam>force_install_dir "c:\rustserver\"
Steam>login anonymous
Steam>app_update 258550
Steam>quit
```

### Configuring and running the server

Batch Script File erstellen: RustServer.bat im Server Install Directory (c:\rustserver) then right click and edit the file.

### The Batch Script File

```
echo off
:start 
C:\steamcmd\steamcmd.exe +login anonymous +force_install_dir c:\rustserver\ +app_update 258550 +quit
RustDedicated.exe -batchmode +server.port 28015 +server.level "Procedural Map" +server.seed 1234 +server.worldsize 4000 +server.maxplayers 10  +server.hostname "Name of Server as Shown on the Client Server List" +server.description "Description shown on server connection window." +server.url "http://yourwebsite.com" +server.headerimage "http://yourwebsite.com/serverimage.jpg" +server.identity "server1" +rcon.port 28016 +rcon.password letmein +rcon.web 1
goto start
```
#### Here is an explanation of each line in the batch file.

`echo off`
This suppresses the console window’s desire to display each command in the batch file as they are executed.

`:start` 
The is a label for a loop starting point.

`C:\steamcmd\steamcmd.exe +login anonymous +force_install_dir c:\rustserver\ +app_update 258550 +quit`
Executes SteamCMD to check for server updates and apply if needed.

`RustDedicated.exe -batchmode +server.port 28015 +server.level "Procedural Map" +server.seed 1234 +server.worldsize 4000 +server.maxplayers 10  +server.hostname "Name of Server as Shown on the Client Server List" +server.description "Description shown on server connection window." +server.url "http://yourwebsite.com" +server.headerimage "http://yourwebsite.com/serverimage.jpg" +server.identity "server1" +rcon.port 28016 +rcon.password letmein +rcon.web 1`
 

`-batchmode`
Opens Unity in non-GUI mode, and eliminates the need for any human intervention.

`+server.port 28015`
Rust client connection port.

`+server.level "Procedural Map"`
The map type to use. Options are "Procedural Map","Barren",”HapisIsland”,”SavasIsland” and “SavasIsland_koth”

`+server.seed 1234`
Determines shape of procedural and barren maps (used with server.worldsize). Values range from 0 to 2147483647.

`+server.worldsize 4000`
Determines shape of procedural and barren maps (used with server.seed). Values range from 1000 to 6000.

`+server.maxplayers 10`
Number of players that can be connected

`+server.hostname "Name of Server as Shown on the Client Server List"`
Name of the server as shown on the client’s server list

`+server.description "Description shown on server connection window."`
Description shown on the client’s server connection window

`+server.url "http://yourwebsite.com"`
A valid website. Causes the “View Webpage” button to appear on the connection window

`+server.headerimage "http://yourwebsite.com/serverimage.jpg"`
A valid link for the connection window background image. Use a JPG image of 512 x 256. 

`+server.identity "server1"`
The directory name used as the parent for all the server files. Do not use spaces or special characters.

`+rcon.port 28016`
Rcon client connection port.

`+rcon.password letmein`
The password required for Rcon access. Do not use spaces or special characters.

`+rcon.web 1`
Uses websocket connection mode for rcon (recommended)

`goto start`
Instructs the batch file to jump to the ‘start’ label. Remove this line if you do not want your server to automatically restart after it shuts down.

## Connecting to your server

Starte RustServer.bat, dauert lange, vor allem das Asset Warmup...

Run the Rust Client, and do not select a server. Note that your server will not show up under the “Local Network” tab. Instead, press F1 and go to the client console. Assuming you used the default port of 28015, type in the following command to connect to your server:

client.connect localhost:28015


## Owners and Moderators

Once the server is up and running you may choose to assign ownership to yourself. This is done with the ownerid command. You will need your 17 digit SteamID number, diese ist in Steam auf der Seite Account direkt unter der Headline. 

The easiest way to get it, is to log in and then run the users command at the console. Then enter the command as follows:

ownerid 12345678901234567 AdminName

For example:

ownerid 12345678901234567 "Admin Name"

You can do the same for moderators using the moderatorid command

moderatorid 12345678901234567 "Admin Name"

Note: As with most commands that allow the use of player names, if the name has spaces or special characters in it, you must use quotes to contain the name.

Be sure to use the writecfg command after doing this and then the person must logout and log back in to receive the permissions. The two permissions are almost identical. Owners can create, kick and ban moderators if needed, but moderators cannot affect owners.

## Gameplay
Waffe nachladen - R


## Cheats

`inventory.give wood 100000`

**Item List:**
https://www.corrosionhour.com/rust-item-list/


https://www.spieletipps.de/tipps-55480-rust-cheats-konsolenbefehle/
https://www.spieletipps.de/tipps-48246-rust-waffen-ruestungsguide/3/
https://www.corrosionhour.com/rust-give-command/
https://wiki.facepunch.com/rust/Creating-a-server


