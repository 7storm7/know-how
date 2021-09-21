# User NOBODY (65534)
It is the most interesting, misupdestood and abused user in linux world.
As a big warning: 

> Some misguided programs or guides suggest that this user should be used for untrusted program execution or handling untrusted data. This is bad advice. Services should have their own, dedicated, user account

Ref: https://wiki.ubuntu.com/nobody

Some info about nobody:
```bash
$ id nobody
uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)

$ getent passwd nobody
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin


# List all processes user nobody is running:
pgrep -u 65534 -a

3787 dnsmasq --port=0 --strict-order --except-interface=lo --interface=cvd-wbr --listen-address=192.168.96.1 --bind-interfaces --dhcp-range=192.168.96.2,192.168.96.255 --dhcp-option=option:dns-server,8.8.8.8,8.8.4.4 --dhcp-option
=option6:dns-server,2001:4860:4860::8888,2001:4860:4860::8844 --conf-file= --pid-file=/var/run/cuttlefish-dnsmasq-cvd-wbr.pid --dhcp-leasefile=/var/run/cuttlefish-dnsmasq-cvd-wbr.leases --dhcp-no-override                         
4321 dnsmasq --port=0 --strict-order --except-interface=lo --interface=cvd-ebr --listen-address=192.168.98.1 --bind-interfaces --dhcp-range=192.168.98.2,192.168.98.255 --dhcp-option=option:dns-server,8.8.8.8,8.8.4.4 --dhcp-option
=option6:dns-server,2001:4860:4860::8888,2001:4860:4860::8844 --conf-file= --pid-file=/var/run/cuttlefish-dnsmasq-cvd-ebr.pid --dhcp-leasefile=/var/run/cuttlefish-dnsmasq-cvd-ebr.leases --dhcp-no-override                         
407139 /lib/systemd/systemd --user                                                                                                                                                                                                   
407140 (sd-pam)                                                                                                                                                                                                                      
407153 sh -c /usr/bin/find / -ignore_readdir_race      \( -fstype NFS -o -fstype nfs -o -fstype nfs4 -o -fstype afs -o -fstype binfmt_misc -o -fstype proc -o -fstype smbfs -o -fstype autofs -o -fstype iso9660 -o -fstype ncpfs -o 
-fstype coda -o -fstype devpts -o -fstype ftpfs -o -fstype devfs -o -fstype mfs -o -fstype shfs -o -fstype sysfs -o -fstype cifs -o -fstype lustre_lite -o -fstype tmpfs -o -fstype usbfs -o -fstype udf -o -fstype ocfs2 -o      -ty
pe d -regex '\(^/tmp$\)\|\(^/usr/tmp$\)\|\(^/var/tmp$\)\|\(^/afs$\)\|\(^/amd$\)\|\(^/alex$\)\|\(^/var/spool$\)\|\(^/sfs$\)\|\(^/media$\)\|\(^/var/lib/schroot/mount$\)' \) -prune -o -print0                                         
407154 /usr/bin/find / -ignore_readdir_race ( -fstype NFS -o -fstype nfs -o -fstype nfs4 -o -fstype afs -o -fstype binfmt_misc -o -fstype proc -o -fstype smbfs -o -fstype autofs -o -fstype iso9660 -o -fstype ncpfs -o -fstype coda
 -o -fstype devpts -o -fstype ftpfs -o -fstype devfs -o -fstype mfs -o -fstype shfs -o -fstype sysfs -o -fstype cifs -o -fstype lustre_lite -o -fstype tmpfs -o -fstype usbfs -o -fstype udf -o -fstype ocfs2 -o -type d -regex \(^/t
mp$\)\|\(^/usr/tmp$\)\|\(^/var/tmp$\)\|\(^/afs$\)\|\(^/amd$\)\|\(^/alex$\)\|\(^/var/spool$\)\|\(^/sfs$\)\|\(^/media$\)\|\(^/var/lib/schroot/mount$\) ) -prune -o -print0                                                             
407157 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only                                                                                                                     
407162 /usr/libexec/gvfsd                                                                                                                                                                                                            
407177 /usr/libexec/gvfsd-fuse /run/user/65534/gvfs -f -o big_writes                                                                                                                                                                 
407185 /usr/libexec/gvfs-udisks2-volume-monitor                                                                                                                                                                                      
407191 /usr/libexec/gvfs-afc-volume-monitor                                                                                                                                                                                          
407196 /usr/libexec/gvfs-gphoto2-volume-monitor                                                                                                                                                                                      
407201 /usr/libexec/gvfs-goa-volume-monitor                                                                                                                                                                                          
407205 /usr/libexec/goa-daemon                                                                                                                                                                                                       
407212 /usr/libexec/goa-identity-service                                                                                                                                                                                             
407219 /usr/libexec/gvfs-mtp-volume-monitor                                                                                                                                                                                          
592066 /usr/libexec/tracker-miner-fs
```

IMPORTANT NOTE:
If you see such output for nobody with full of find command executions, then you should do something with **locate** command. As mentioned in [nobody running updatedb|https://askubuntu.com/questions/514911/why-nobody-always-starts-a-new-find-program-that-always-consume-my-memory], locate command has a service that is running sometimes to update its database by checking all the filesystems exist.
And it can cause some weird problems while you are using ccache while building an application.
e.g: I had that issue while I was trying to build a native application in AOSP:

```bash
...
ccache: error: Failed to create directory /run/user/65534/ccache-tmp: Permission denied
08:57:37 ninja failed with: exit status 1
```
So, if it happens, kill all the processes nobody is running and bury the updatedb daemon deep down inside :)


# Filesystem Hierarchy Standard
It defines the directory structure and directory contents in Linux distributions.[1] It is maintained by the Linux Foundation. The latest version is 3.0, released on 3 June 2015.[2]

Linux distributions (and other operating systems) **_can voluntarily conform to the FHS_**. The Freedesktop.org project, with its XDG Base Directory Specification, introduced variables to make a computer's file system hierarchy configurable, for users.

Ref: https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard

