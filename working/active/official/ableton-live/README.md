# Ableton Live
(Last tested: 12th of October, 2023 on Garuda Linux Raptor)

Getting Live to run on Linux is easy, but you'll need to make sure a few things are installed first:
- `wine-staging` (regular `wine` should work too, but we test with `wine-staging`)
- `winetricks`
- `winbind` (from `samba` package if you use an Arch-based distro)
- `pipewire-jack`
- `wineasio` (on Arch-based distros, `wineasio` can be found in the `chaotic-aur` repository)
- `qpwgraph`

Now just follow these simple steps:


1. Open Winetricks and create a new 64-bit prefix, name it what you like, I named mine `abletonlive`, and that is the name this guide will use
2. Select "Install a Windows DLL or component"
3. Locate and install each of these:
    
    ⚠️ Make sure to install the exact versions. For instance, find `dxvk` specifically, not `dxvk2010` or any other version
    
    ⚠️ It might take a while. Be patient!

    ℹ️ It will close while it's installing, and then return you back to the Winetricks menu, be sure to click on "Install a Windows DLL or component" again.
    - `vcrun2015`
    - `quicktime72`
    - `dxvk`
    - `quartz`
4. Select "Run winecfg"
5. Go to Applications > Windows Version, and select "Windows 7"
    
    ℹ️ We haven't yet tested other Windows version settings, but they may work.
6. Select "OK" to return to Winetricks. You may now close Winetricks if you wish
7. Open up a terminal, and go (using `cd`) to where you extracted the Live installer.
8. Run `WINEPREFIX=~/.local/share/wineprefixes/abletonlive wineasio-register`
9. Run `WINEPREFIX=~/.local/share/wineprefixes/abletonlive wine 
"installer_name_here"`

    ❌ **Never run Wine with `sudo`! You risk harming your system! [Learn More](https://askubuntu.com/questions/947772/why-is-running-wine-with-sudo-dangerous)**

    ⚠️ Change `abletonlive` to whatever you named your prefix

    ⚠️ Change `installer_name_here` to the installer's filename. Make sure to add the `.exe` at the end, and put quotes on either side.
10. Go through the installer as usual

    ⚠️ It  may appear to be frozen for up to 3 minutes. If this happens, just wait
11. Once you get in, set up Ableton as you would on Windows
12. Set up ASIO as you would on Windows, but make sure to set the driver to "WineASIO Driver"
13. Open qpwgraph
14. Connect your inputs and outputs to "Ableton Live".
    
    ℹ️ The name may vary but will always contain Ableton Live

15. Set up your audio inputs as you would on Windows.


Just like that, you're done! Ableton should be all set up, and should run smoothly. But in case it doesn't...

## Troubleshooting
### Audio freezes and then comes back after a few seconds (buffer XRUNs)
Go to the Audio Settings in Live, and select "Hardware Setup", and tick "Fixed buffersize". Increase the "preferred buffersize" and hit "OK" until the freezes stop. 

⚠️ Doing this will increase latency.

### Audio latency is bad!
First, make sure you are using ASIO and the driver is set to "WineASIO Driver"

Then, go to the Audio Settings in Live, and select "Hardware Setup", and tick "Fixed buffersize". Decrease the "preferred buffersize" and hit "OK" until the audio latency is good.

⚠️ Doing this increases CPU load.

### I have another problem!
Just raise an issue!