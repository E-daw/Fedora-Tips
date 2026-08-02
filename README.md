# Fedora-Tips

    In your bios, disable unused services features, and controllers like your CPUs iGPU, ethernet if you use wifi, etc.

    Enable fast boot: CAUTION... sometimes this can introduce stability and firmware issues. Hardware may not be initialized on boot.

    
    sudo fstrim -av //Runs fstrim on command.

    

Software to Install:
--------------------

    sudo dnf install kate               //installs the kate text editor.
    sudo dnf install corectrl           //Overclocking and hardware management software.
    sudo dnf install fastfetch          //Instant hardware info grabbing software
    sudo dnf install btop               //Terminal based task manager, highly configurable.
    sudo dnf install gamescope          //Micro compositor for launching games.
    flatpak install gpu_screen_recorder //Best screen recording utility with lots of configuration.




Gaming/ Workstation PC:
-----------------------
  Disable NetowrkManager-wait-online
  
    sudo systemctl disable NetworkManager-wait-online.service //This can hang boot times by a few seconds, leave enabled if you know you need it.
  

  Enable fstrim to automatically run:
  
    sudo systemctl enable --now fstrim.timer
  

  Set the performance profile to high:
  
    sudo tuned-adm profile latency-performance //Best overall profile for hardware performance.
    
    tuned-adm active //Run to verify previous command worked.

    kate /etc/tuned/ppd.conf //ensure that performance=throughput-performance. Save and exit.

    If running a game server... use the network-latency profile instead of latency-performance.

  Disable Split Lock mitigation:

  Split lock mitigation is a security feature. It's used to prevent exploits when running software through emulation like proton. It's
  not completely necessary when running games through proton.

    sudo grubby --update-kernel=ALL --args="split_lock_detect=off"

  Allow AMD GPU overclocking.
  
      sudo grubby --update-kernel=ALL --args="amdgpu.ppfeaturemask=0xffffffff"
      
  Disable ModemManager:

  This is cellular modem service, it's not necessary for WiFi/Ethernet users.

      sudo systemctl disable ModemManager.service

  Dracut optimization:
  
  Fedora packages many drivers with the install to accomidate many machines. Use these commands to build a lighter
  OS image that's tailored more to your PC's hardware. This doesn't remove anything and you will maintain compatability with other       hardware when running these commands again. Running these can improve boot times.

      echo 'hostonly="yes"' | sudo tee /etc/dracut.conf.d/hostonly.conf

      sudo dracut --regenerate-all --force


  Gamemode:

  Gamemode optmizes a few settings in the OS for games. It's mostly obsolete but running it doesn't hurt.

      systemctl --user enable gamemoded.service

  Place the command "gamemoderun" in your launch arguments for the desired steam game.

  Gamescope:

  Gamescope is a micro compositor. Use it if games feel like they have latency or you just want better response times.

  Per game in steam, place this command in your launch arguments...

      gamescope -f -W 3840 -H 2160 -r 240 --rt -- gamemoderun %command% //Replace parameters with your monitors resolution and refreshrate. This should be used for the majority of your games.

      gamescope -f -w 2560 -h 1440 -W 3840 -H 2160 -r 240 -F fsr --hdr-enabled --adaptive-sync -- %command% //Example with FSR, HDR and adaptive sync. NOTE for FSR, this only uses FSR 1.0. If the game features a higher version please use that instead. The first two integer parameters are the input resolution for FSR. This example would be near the "Quality" slider.

      --force-grab-cursor
      --hdr-enabled
      --adaptive-sync
      --rt
      --force-grab-cursor //Use if the cursor's effective interaction point is offset.
  
      
      

    
