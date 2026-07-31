# Fedora-Tips

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
  
    *sudo systemctl disable NetworkManager-wait-online.service* //This can hang boot times by a few seconds, leave enabled if you know you need it.
  

  Enable fstrim to automatically run
  
    *sudo systemctl enable --now fstrim.timer*
  

  Set the performance profile to high.
  
    *sudo tuned-adm profile latency-performance* //Best overall profile for hardware performance.
    
    *tuned-adm active* //Run to verify previous command worked.

    kate /etc/tuned/ppd.conf //ensure that performance=throughput-performance. Save and exit.

    If running a game server... use the network-latency profile instead of latency-performance.
    
