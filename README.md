# Fedora-Tips

sudo fstrim -av //Runs fstrim on command.
sudo dnf install kate //installs the kate text editor.




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
    
