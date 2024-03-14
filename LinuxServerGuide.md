# Linux Dedicated Server

### Running via AMP
There is a Dead Matter template already in [AMP](https://cubecoders.com/AMP) that will configure and monitor your server for you. It is reccomended to run the new instance inside Docker - this way all dependancies are pre-installed for you. This can be configured within AMP. 

*Note, this is a paid product.*

1) Make sure your AMP is up to date
2) Create a new instance (Dead Matter will be in the list)
3) Follow usual AMP processes to update the server, configure settings, then run

### Running Manually
**It is not reccomended to run as root. Create a dedicated user to run the server first.**
1) Install Wine:

    `sudo apt update`
   
    `sudo apt install wine`

2) Download Server Files
    * Log in as your server user and create a folder for SteamCMD: `mkdir $HOME/steamcmd`
    * Download SteamCMD: `wget -P $HOME/steamcmd https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz`
    * Unpack: `tar -xzvf $HOME/steamcmd/steamcmd_linux.tar.gz -C $HOME/steamcmd/`
    * Download the server files: `$HOME/steamcmd/steamcmd.sh +@sSteamCmdForcePlatformType windows +force_install_dir ~/DeadMatter +login anonymous +app_update 2584780 validate +quit`
    * Download SteamSDK: `$HOME/steamcmd/steamcmd.sh +@sSteamCmdForcePlatformType windows +force_install_dir ~/DeadMatter/DeadMatter/Binaries/Win64 +login anonymous +app_update 1007 validate +quit`
3) Launch the server (assumptions that you understand how to run in screens etc)
    * Set the Wine prefix and arch with `WINEPREFIX="$/HOME.wine" WINEARCH=win64"`
    * Navigate to the binary folder`cd $HOME/DeadMatter/DeadMatter/Binaries/Win64/`
    * Start the server with: `wine ./DeadMatterServer-Win64-Test.exe DeadMatter -stdout -FullStdOutLogOutput -Port=7777 -QueryPort=7778 -SteamServerName="My Server Name" -MaxPlayers="32" -Wait`

### Known Issues with Wine
 * **Out of Memory**  - If Wine crashes whilst booting the server with an *Out of Memory* error then you will need to increase your max_map_count. To do this, ssh into your server as **root** and run `bash -c 'echo "vm.max_map_count = 16777216" > /etc/sysctl.d/20-max_map_count.conf && sysctl --system'`. Then try running the server again.
