# MC-Eternal-Server-Tips
Minecraft Eternal Server Tips

Eternal server side configs, etc

--- Recommended things ---

Disable spike_creative: 
in \config\extrautils2.cfg
    B:spike_creative=false

Disable giant chance cube things:
in config\ChanceCubes\chancecubes.cfg
giant chance cube rewards" {
    B:"chancecubes:Chunk_Flip"=false
the main horrible one is chunk_flip.. but disable other ones if you dont like them.

Remove deaths for named entities:
Disable this config in config\cofh\core\common.cfg
B:EnableGenericDeathMessage=true

Added server side mods:
chunkgenlimiter-1.1.jar (this will limit lag from exploration)
worldprimer-1.12.2-??.jar (I use for repeating commands automatically on a timer)
forgeautoshutdown-1.12.2-1.0.0.jar (Shut down server on timer, you need a startup wrapper like the windows one below to start it again though)
spark-forge (performance profiling)
labgonreborn (I use for chunk lag, clears unused chunks on time interval)
unloader-1.2.0 (this unloads dimensions that arent used on timed interval)

Settings for mods:
chunkgenlimiter:
leave as-is

worldprimer:
add this for auto-icbmc gravity block entity removal every hour 
    S:timedCommands <
	worldprimer-timed-command %120000 0 say ICBMC gravity blocks cleared.
	worldprimer-timed-command %120000 0 icbmc remove all

forgeautoshutdown
S:Kick=Scheduled server restart
S:Warn=Server is restarting in %m minute(s).
I:Hour=6 
(You can change the hour/minutes to whatever you prefer)

lagbgonreborn
B:AutomaticRemoval=false
I:Interval=60
I:TPSForUnload=15
I:Unload=15

unloader
leave as default

-- Useful commands --

/chunks unload_everything, resets all loaded chunks by players
/forge entity list, shows entities in that world
/mc remove colony: 1 , it needs the space between colony: and 1, it will remove colony #1
/bgon unload , /bgon automatic
/icbmc remove all , gets rid of icbm entity lag that seems to pop up now and then.

Fixes from #tips for 1.3.7.1 I dont know if these are needed for 1.4
compactcoins.zs
starmetalfix.zs
world-gen.json

-- Wrapper script for windows server --
Add this in a .bat file, use to launch server. It will start server if server is stopped or crashed. Java args can be whatever you prefer.

@echo off
cls
echo This script will keep your server running even after crashing!
title Minecraft WatchDog
:StartServer
start /wait java -Xmx10G -Xms10G -Xss8M -Dfile.encoding=GBK -Dsun.rmi.dgc.server.gcInterval=1800000 -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:G1NewSizePercent=20 -XX:G1ReservePercent=20 -XX:MaxGCPauseMillis=50 -XX:+AlwaysPreTouch -XX:+UseStringDeduplication -Dfml.ignorePatchDiscrepancies=true -Dfml.ignoreInvalidMinecraftCertificates=true -XX:-OmitStackTraceInFastThrow -XX:+OptimizeStringConcat -XX:+UseAdaptiveGCBoundary -XX:G1HeapRegionSize=32M -jar forge-1.12.2-14.23.5.2847-universal.jar nogui -o true
echo (%time%) Server closed/crashed... restarting!
goto StartServer
pause

You can also go a step further and use windows task scheduler to auto-start this .bat if the physical/vm server reboots for any reason

--- Try these things if you have problems or like to tinker, these are mostly black magic ---

No more fast leaf decay or messages: 
delete fastleafdecay jar from \mods)

Disable Biliocraft bookshelf: 
\config\bibliocraft.cfg , B:Bookcase=false

Change forge.cfg, dimension unload 
clumpingThreshold=128
I:dimensionUnloadQueueDelay=5

Change forgechunkload.cfg
I:maximumChunksPerTicket=75
I:maximumTicketCount=350
I:playerTicketCount=600

