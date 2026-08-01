# Fedora-Tips

    In your bios, disable unused services features, and controllers like your CPUs iGPU, ethernet if you use wifi, etc.

    Enable fast boot: CAUTION... sometimes this can introduce stability and firmware issues. Hardware may not be initialized on boot.

    
    sudo fstrim -av //Runs fstrim on command.

Software to Install:
--------------------

    sudo dnf install kate               //installs the kate text editor.
    sudo dnf install corectrl           //Overclocking and hardware management software.
    sudo dnf install fastfetch          //Instant hardware info grabbing software
    sudo dnf install btop               //Terminal based task manager, highly configurable
    flatpak install gpu_screen_recorder //Best screen recording utility with lots of configuration




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

    sudo grubby --update-kernel=ALL --args="split_lock_detect=off" //Split lock mitigation is a security feature.

  Allow AMD GPU overclocking.
  
      sudo grubby --update-kernel=ALL --args="amdgpu.ppfeaturemask=0xffffffff"
      
  Disable ModemManager:

      sudo systemctl disable ModemManager.service //This is cellular modem service, it's not necessary for WiFi/Ethernet

  Dracut optimization:
  Fedora packages many drivers with the install to accomidate many machines. Use these commands to build a lighter
  OS image that's tailored more to your PC's hardware. This doesn't remove anything and you will maintain compatability with other       hardware when running these commands again.

      echo 'hostonly="yes"' | sudo tee /etc/dracut.conf.d/hostonly.conf

      sudo dracut --regenerate-all --force
      
      

    
