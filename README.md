# MC-Eternal-Server-Tips <br />
Eternal server side configs, etc  <br />
Most of these are tested on 1.3.7.1, however should mostly work on 1.4.x  <br />

**--- Recommended things ---  <br />**

Disable spike_creative:  <br />
in \config\extrautils2.cfg  <br />
    B:spike_creative=false  <br />

Disable giant chance cube things:  <br />
in config\ChanceCubes\chancecubes.cfg  <br />
giant chance cube rewards" {  <br />
    B:"chancecubes:Chunk_Flip"=false  <br />
the main horrible one is chunk_flip.. but disable other ones if you dont like them.  <br />

Remove deaths for named entities:  <br />
Disable this config in config\cofh\core\common.cfg  <br />
B:EnableGenericDeathMessage=true  <br />

Added server side mods:  <br />
chunkgenlimiter-1.1.jar (this will limit lag from exploration)  <br />
worldprimer-1.12.2-??.jar (I use for repeating commands automatically on a timer)  <br />
forgeautoshutdown-1.12.2-1.0.0.jar (Shut down server on timer, you need a startup wrapper like the windows one below to start it again though)  <br />
spark-forge (performance profiling)  <br />
labgonreborn (I use for chunk lag, clears unused chunks on time interval)  <br />
unloader-1.2.0 (this unloads dimensions that arent used on timed interval)  <br />

Settings for mods:  <br />
chunkgenlimiter:  <br />
leave as-is  <br />

worldprimer:  <br />
add this for auto-icbmc gravity block entity removal every hour   <br />
    S:timedCommands <  <br />
	worldprimer-timed-command %120000 0 say ICBMC gravity blocks cleared.  <br />
	worldprimer-timed-command %120000 0 icbmc remove all  <br />

forgeautoshutdown  <br />
S:Kick=Scheduled server restart  <br />
S:Warn=Server is restarting in %m minute(s).  <br />
I:Hour=6   <br />
(You can change the hour/minutes to whatever you prefer)  <br />

lagbgonreborn  <br />
B:AutomaticRemoval=false  <br />
I:Interval=60  <br />
I:TPSForUnload=15  <br />
I:Unload=15  <br />

unloader  <br />
leave as default  <br />

Server.Properties  <br />
    Set server view distance to 7  <br />
    
appliedenergistics2.cfg  <br />
I:craftingCalculationTimePerTick=1  <br />

**-- Useful commands --  <br />**

/chunks unload_everything, resets all loaded chunks by players  <br />
/forge entity list, shows entities in that world  <br />
/mc remove colony: 1 , it needs the space between colony: and 1, it will remove colony #1  <br />
/bgon unload , /bgon automatic  <br />
/icbmc remove all , gets rid of icbm entity lag that seems to pop up now and then.  <br />
/cofh tps 0  <br />
For live ingame display of TPS for all dimensions and other interesting data, use tool called "chunk-pregenerator". To enable, go to Options Gui in Controls.  <br />
set the hotkey for that, open it up, there will be a TrackerUI options, click that, and also click "enable Tracker Gui". You need to be opped to see info I believe.  <br />

Fixes from #tips for 1.3.7.1 I dont know if these are needed for 1.4  <br />
compactcoins.zs  <br />
starmetalfix.zs  <br /> 
world-gen.json  <br />

**-- Wrapper script for windows server --  <br />**
Add this in a .bat file, use to launch server. It will start server if server is stopped or crashed. Java args can be whatever you prefer.  <br />

@echo off  <br />
cls  <br />
echo This script will keep your server running even after crashing! <br />
title Minecraft WatchDog <br />
:StartServer <br />
start /wait java -Xmx10G -Xms10G -Xss8M -Dfile.encoding=GBK -Dsun.rmi.dgc.server.gcInterval=1800000 -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:G1NewSizePercent=20 -XX:G1ReservePercent=20 -XX:MaxGCPauseMillis=50 -XX:+AlwaysPreTouch -XX:+UseStringDeduplication -Dfml.ignorePatchDiscrepancies=true -Dfml.ignoreInvalidMinecraftCertificates=true -XX:-OmitStackTraceInFastThrow -XX:+OptimizeStringConcat -XX:+UseAdaptiveGCBoundary -XX:G1HeapRegionSize=32M -jar forge-1.12.2-14.23.5.2847-universal.jar nogui -o true  <br />
echo (%time%) Server closed/crashed... restarting!  <br />
goto StartServer <br />
pause <br />

You can also go a step further and use windows task scheduler to auto-start this .bat if the physical/vm server reboots for any reason <br />

--- Try these things if you have problems or like to tinker, these are mostly black magic --- <br />

No more fast leaf decay or messages:  <br />
delete fastleafdecay jar from \mods) <br />

Disable Biliocraft bookshelf:  <br />
\config\bibliocraft.cfg , B:Bookcase=false <br />

Change forge.cfg, dimension unload  <br />
clumpingThreshold=128 <br />
I:dimensionUnloadQueueDelay=5 <br />

Change forgechunkload.cfg <br />
I:maximumChunksPerTicket=75 <br />
I:maximumTicketCount=350 <br />
I:playerTicketCount=600 <br />

**--- These are from official discord, I have not tested all of them. I have heard using spongeforge can create new issues --- <br />**
 
Config Changes <br />
------------------------ <br />

Added Spongeforge - spongeforge-1.12.2-2838-7.1.9 <br />

Rename Spongeforge Jar file to _aaaaaSpongeforge.jar <br />

Replace Lag Goggles with THIN version (For Spongeforge)** (As for now Lag Goggles are not working with SpongeForge 7.1.9 - Do not use with this version) <br />

Disabled The Summoner - Depends on multimob, adds 1 mob <br />
Disabled Primitive Mobs - Buggy as hell, Lags really bad, Depends on multimob <br />
Disabled Multimob - Complete and utter poo, causes more issues than its worth <br />
Disabled Farseek - Streams Coremod <br />
Disabled Streams - Prone to Laggyness <br />

Sponge config <br />
    Changed per player enemy spawning: (spawn-limit-monster=30 <70) <br />
    Changed Dimension Spawn Loading: (keep-spawn-loaded=false) <br />
    Changed all dimensions from being loaded on server start (/config/sponge/worlds/*) <br />
    
Foamfix: <br />
    B:optimizedBlockPos=false <br />
    B:patchChunkSerialization=false <br />

Config Change: <br />
    Dungeons2: changed rarity and spawn distance: (I:dungeonGenProbability=15 <35 -- I:minChunksPerDungeon=500 <300) <br />
    Fish's Undead Rising: changed spawn rate: (I:"piranha spawn rate"=20 <2 -- I:"raven spawn rate"=20 <8) <br />
    Ruins: Changed rarity: (anyRuinsMinDistance=128 <64) <br />
