# Fedora-Tips

Gaming/ Workstation PC:
-----------------------
  Things to Disable
    *sudo systemctl disable NetworkManager-wait-online.service* //This can hang boot times by a few seconds, leave enabled if you know you need it.
  
  Things to Enable
    *sudo systemctl enable --now fstrim.timer*
  
  Commands to Run
    *sudo tuned-adm profile latency-performance* //Best overall profile for hardware performance.
    *tuned-adm active* //Run to verify previous command worked.

Game Server:
------------
  Things to Disable
    *sudo systemctl disable NetworkManager-wait-online.service* //This can hang boot times by a few seconds, leave enabled if you know you need it.
  
  Things to Enable
    *sudo systemctl enable --now fstrim.timer*
  
  Commands to Run
    *sudo tuned-adm profile network-latency* //Best overall profile for hardware and network performance.
    *tuned-adm active* //Run to verify previous command worked.
