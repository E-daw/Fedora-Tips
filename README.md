# Fedora-Tips

In your bios, disable unused services features, and controllers like your CPUs iGPU, ethernet if you use wifi, etc.

Enable fast boot: CAUTION... sometimes this can introduce stability and firmware issues. Hardware may not be initialized on boot.

# Useful commands:

Trims your storage drive WARNING: Might take some time to complete

    sudo fstrim -av
Update your computer and software packages

    sudo dnf upgrade --refresh
Update flatpak packages

    flatpak upgrade

    

# Software to Install:

    sudo dnf install kate               //installs the kate text editor.
    sudo dnf install corectrl           //Overclocking and hardware management software.
    sudo dnf install fastfetch          //Instant hardware info grabbing software
    sudo dnf install btop               //Terminal based task manager, highly configurable.
    sudo dnf install gamescope          //Micro compositor for launching games.
    sudo dnf install steam
    sudo dnf install iwd                //Better WiFi driver.
    sudo dnf install kden-live          //Video editing software.
    
    flatpak install discord
    flatpak install gpu_screen_recorder //Best screen recording utility with lots of configuration.

# Gaming/ Workstation PC:

  Disable NetowrkManager-wait-online

  This can hang boot times by a few seconds, leave enabled if you know you need it.
  
    sudo systemctl disable NetworkManager-wait-online.service 

  Enable fstrim to automatically run:
  
    sudo systemctl enable --now fstrim.timer
  

  Set the performance profile to high:

  Best overall profile for hardware performance.
  
    sudo tuned-adm profile latency-performance 

Run to verify previous command worked.
    
    tuned-adm active 
    
ensure that performance=throughput-performance. Save and exit.

    kate /etc/tuned/ppd.conf 

If running a game server... use the network-latency profile instead of latency-performance.

  Disable Split Lock mitigation:
  ------------------------------

  Split lock mitigation is a security feature. It's used to prevent exploits when running software through emulation like proton. It's
  not completely necessary when running games through proton.

    sudo grubby --update-kernel=ALL --args="split_lock_detect=off"

  Allow AMD GPU overclocking:
  ---------------------------
    sudo grubby --update-kernel=ALL --args="amdgpu.ppfeaturemask=0xffffffff"
      
  Disable ModemManager:
  ---------------------

  This is cellular modem service, it's not necessary for WiFi/Ethernet users.

    sudo systemctl disable ModemManager.service

  Dracut optimization:
  --------------------
  
  Fedora packages many drivers with the install to accomidate many machines. Use these commands to build a lighter
  OS image that's tailored more to your PC's hardware. This doesn't remove anything and you will maintain compatability with other       hardware when running these commands again. Running these can improve boot times.

    echo 'hostonly="yes"' | sudo tee /etc/dracut.conf.d/hostonly.conf
.

    sudo dracut --regenerate-all --force


  Gamemode:
  ---------

  Gamemode optmizes a few settings in the OS for games. It's mostly obsolete but running it doesn't hurt.

    systemctl --user enable gamemoded.service

  Place the command "gamemoderun" in your launch arguments for the desired steam game.

  Gamescope:
  ----------

  Gamescope is a micro compositor. Use it if games feel like they have latency/stuttering issues or misbehave with scaling. Gamescope works best with titles that aren't supported well on proton or are just old.

  Per game in steam, place this command in your launch arguments...
  
Replace parameters with your monitors resolution and refreshrate. This should be used for the majority of your games.

    gamescope -f -W 3840 -H 2160 -r 240 -- gamemoderun %command%

Example with FSR, HDR and adaptive sync. NOTE for FSR, this only uses FSR 1.0. If the game features a higher version please use that instead. The first two integer parameters are the input resolution for FSR. This example would be near the "Quality" slider.

    gamescope -f -w 2560 -h 1440 -W 3840 -H 2160 -r 240 -F fsr --hdr-enabled --adaptive-sync -- %command% 

      --force-grab-cursor
      --hdr-enabled
      --adaptive-sync
      --force-grab-cursor //Use if the cursor's effective interaction point is offset.

CachyOS Kernel:
---------------
The CatchyOS kernel can maximize system responsiveness and minimize latency. the CachyOS kernel uses BORE CPU Scheduler which is more suitable for tasks like gaming.

First check if your CPU is compatible. It needs to say x86_64_v3 or higher, otherwise DO NOT CONTINUE.

    /lib64/ld-linux-x86-64.so.2 --help | grep "(supported, searched)"
If you see x86_64_v3 continue. The next command enables custom kernels to run on your operating system.

    sudo setsebool -P domain_kernel_load_modules on
The next commands install the kernel.

    sudo dnf copr enable bieszczaders/kernel-cachyos-lto
    sudo dnf install kernel-cachyos-lto kernel-cachyos-lto-devel-matched

Next, reboot, and you should finished.

    sudo systemctl reboot

You can use the fastfetch command or uname-r to see if the CatchyOS kernel is running.

Networking with IWD:
--------------------
wpa_supplicant is reliable but not very fast or effecient. Switching to IWD can fix network latency issues found in gaming.

Start by installing iwd.

    sudo dnf install iwd
      
      

    
