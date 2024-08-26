# Install VM with CentOS 9, Oracle 21c and PostgreSQL

## Install Oracle 21c

* compat-openssl10-1.0.2u-1.el9.x86_64.rpm
* oracle-database-ee-21c-1.0-1.ol8.x86_64.rpm
* oracle-database-preinstall-21c-1.0-1.el8.x86_64.rpm


```bash
[root@centos9s distr]# ls
compat-openssl10-1.0.2u-1.el9.x86_64.rpm  oracle-database-ee-21c-1.0-1.ol8.x86_64.rpm  oracle-database-preinstall-21c-1.0-1.el8.x86_64.rpm
[root@centos9s distr]# rpm -i compat-openssl10-1.0.2u-1.el9.x86_64.rpm
warning: compat-openssl10-1.0.2u-1.el9.x86_64.rpm: Header V4 RSA/SHA256 Signature, key ID 2dcd03a2: NOKEY
[root@centos9s distr]# dnf localinstall oracle-database-preinstall-21c-1.0-1.el8.x86_64.rpm
Last metadata expiration check: 0:00:38 ago on Sat 24 Aug 2024 03:53:55 PM UTC.
Dependencies resolved.
======================================================================================================================================================
 Package                                           Architecture              Version                            Repository                       Size
======================================================================================================================================================
Installing:
 oracle-database-preinstall-21c                    x86_64                    1.0-1.el8                          @commandline                     30 k
Installing dependencies:
 bc                                                x86_64                    1.07.1-14.el9                      baseos                          120 k
 checkpolicy                                       x86_64                    3.6-1.el9                          baseos                          353 k
 chkconfig                                         x86_64                    1.24-1.el9                         baseos                          179 k
 gssproxy                                          x86_64                    0.8.4-7.el9                        baseos                          110 k
 initscripts                                       x86_64                    10.11.7-1.el9                      baseos                          228 k
 ksh                                               x86_64                    3:1.0.6-3.el9                      appstream                       880 k
 libX11-xcb                                        x86_64                    1.7.0-9.el9                        appstream                        11 k
 libXcomposite                                     x86_64                    0.4.5-7.el9                        appstream                        24 k
 libXi                                             x86_64                    1.7.10-8.el9                       appstream                        40 k
 libXinerama                                       x86_64                    1.1.4-10.el9                       appstream                        15 k
 libXrandr                                         x86_64                    1.5.2-8.el9                        appstream                        28 k
 libXrender                                        x86_64                    0.9.10-16.el9                      appstream                        28 k
 libXtst                                           x86_64                    1.2.3-16.el9                       appstream                        21 k
 libXv                                             x86_64                    1.0.11-16.el9                      appstream                        19 k
 libXxf86dga                                       x86_64                    1.1.5-8.el9                        appstream                        21 k
 libXxf86vm                                        x86_64                    1.1.4-18.el9                       appstream                        19 k
 libdmx                                            x86_64                    1.1.4-12.el9                       appstream                        17 k
 libev                                             x86_64                    4.33-5.el9                         baseos                           53 k
 libnfsidmap                                       x86_64                    1:2.5.4-27.el9                     baseos                           61 k
 libnsl                                            x86_64                    2.34-120.el9                       baseos                           64 k
 libverto-libev                                    x86_64                    0.3.2-3.el9                        baseos                           14 k
 nfs-utils                                         x86_64                    1:2.5.4-27.el9                     baseos                          459 k
 policycoreutils-python-utils                      noarch                    3.6-2.1.el9                        appstream                        77 k
 python3-audit                                     x86_64                    3.1.5-1.el9                        appstream                        83 k
 python3-distro                                    noarch                    1.5.0-7.el9                        baseos                           37 k
 python3-libsemanage                               x86_64                    3.6-1.el9                          baseos                           80 k
 python3-policycoreutils                           noarch                    3.6-2.1.el9                        appstream                       2.1 M
 python3-pyyaml                                    x86_64                    5.4.1-6.el9                        baseos                          205 k
 python3-setools                                   x86_64                    4.4.4-1.el9                        baseos                          605 k
 python3-setuptools                                noarch                    53.0.0-13.el9                      baseos                          943 k
 quota                                             x86_64                    1:4.09-2.el9                       baseos                          198 k
 quota-nls                                         noarch                    1:4.09-2.el9                       baseos                           77 k
 rpcbind                                           x86_64                    1.2.6-7.el9                        baseos                           58 k
 smartmontools                                     x86_64                    1:7.2-9.el9                        baseos                          557 k
 sssd-nfs-idmap                                    x86_64                    2.9.5-4.el9                        baseos                           42 k
 xorg-x11-utils                                    x86_64                    7.5-40.el9                         appstream                       110 k
 xorg-x11-xauth                                    x86_64                    1:1.1-10.el9                       appstream                        37 k

Transaction Summary
======================================================================================================================================================
Install  38 Packages

Total size: 7.9 M
Total download size: 7.8 M
Installed size: 26 M
Is this ok [y/N]: y
Downloading Packages:
(1/37): chkconfig-1.24-1.el9.x86_64.rpm                                                                               219 kB/s | 179 kB     00:00
(2/37): checkpolicy-3.6-1.el9.x86_64.rpm                                                                              426 kB/s | 353 kB     00:00
(3/37): initscripts-10.11.7-1.el9.x86_64.rpm                                                                          1.5 MB/s | 228 kB     00:00
(4/37): gssproxy-0.8.4-7.el9.x86_64.rpm                                                                               638 kB/s | 110 kB     00:00
(5/37): libev-4.33-5.el9.x86_64.rpm                                                                                   458 kB/s |  53 kB     00:00
(6/37): libnfsidmap-2.5.4-27.el9.x86_64.rpm                                                                           532 kB/s |  61 kB     00:00
(7/37): bc-1.07.1-14.el9.x86_64.rpm                                                                                   108 kB/s | 120 kB     00:01
(8/37): libnsl-2.34-120.el9.x86_64.rpm                                                                                601 kB/s |  64 kB     00:00
(9/37): libverto-libev-0.3.2-3.el9.x86_64.rpm                                                                         134 kB/s |  14 kB     00:00
(10/37): nfs-utils-2.5.4-27.el9.x86_64.rpm                                                                            2.4 MB/s | 459 kB     00:00
(11/37): python3-distro-1.5.0-7.el9.noarch.rpm                                                                        353 kB/s |  37 kB     00:00
(12/37): python3-libsemanage-3.6-1.el9.x86_64.rpm                                                                     624 kB/s |  80 kB     00:00
(13/37): python3-setools-4.4.4-1.el9.x86_64.rpm                                                                       1.3 MB/s | 605 kB     00:00
(14/37): python3-pyyaml-5.4.1-6.el9.x86_64.rpm                                                                        439 kB/s | 205 kB     00:00
(15/37): python3-setuptools-53.0.0-13.el9.noarch.rpm                                                                  2.1 MB/s | 943 kB     00:00
(16/37): quota-4.09-2.el9.x86_64.rpm                                                                                  1.2 MB/s | 198 kB     00:00
(17/37): rpcbind-1.2.6-7.el9.x86_64.rpm                                                                               293 kB/s |  58 kB     00:00
(18/37): quota-nls-4.09-2.el9.noarch.rpm                                                                              319 kB/s |  77 kB     00:00
(19/37): smartmontools-7.2-9.el9.x86_64.rpm                                                                           3.3 MB/s | 557 kB     00:00
(20/37): sssd-nfs-idmap-2.9.5-4.el9.x86_64.rpm                                                                        394 kB/s |  42 kB     00:00
(21/37): libX11-xcb-1.7.0-9.el9.x86_64.rpm                                                                             38 kB/s |  11 kB     00:00
(22/37): libXcomposite-0.4.5-7.el9.x86_64.rpm                                                                          82 kB/s |  24 kB     00:00
(23/37): libXinerama-1.1.4-10.el9.x86_64.rpm                                                                          945 kB/s |  15 kB     00:00
(24/37): libXi-1.7.10-8.el9.x86_64.rpm                                                                                1.4 MB/s |  40 kB     00:00
(25/37): libXrandr-1.5.2-8.el9.x86_64.rpm                                                                             347 kB/s |  28 kB     00:00
(26/37): libXrender-0.9.10-16.el9.x86_64.rpm                                                                          351 kB/s |  28 kB     00:00
(27/37): ksh-1.0.6-3.el9.x86_64.rpm                                                                                   1.7 MB/s | 880 kB     00:00
(28/37): libXtst-1.2.3-16.el9.x86_64.rpm                                                                              716 kB/s |  21 kB     00:00
(29/37): libXv-1.0.11-16.el9.x86_64.rpm                                                                               670 kB/s |  19 kB     00:00
(30/37): libXxf86vm-1.1.4-18.el9.x86_64.rpm                                                                           795 kB/s |  19 kB     00:00
(31/37): libXxf86dga-1.1.5-8.el9.x86_64.rpm                                                                           508 kB/s |  21 kB     00:00
(32/37): libdmx-1.1.4-12.el9.x86_64.rpm                                                                               521 kB/s |  17 kB     00:00
(33/37): python3-audit-3.1.5-1.el9.x86_64.rpm                                                                         3.5 MB/s |  83 kB     00:00
(34/37): policycoreutils-python-utils-3.6-2.1.el9.noarch.rpm                                                          2.0 MB/s |  77 kB     00:00
(35/37): xorg-x11-utils-7.5-40.el9.x86_64.rpm                                                                         3.4 MB/s | 110 kB     00:00
(36/37): xorg-x11-xauth-1.1-10.el9.x86_64.rpm                                                                         970 kB/s |  37 kB     00:00
(37/37): python3-policycoreutils-3.6-2.1.el9.noarch.rpm                                                               4.0 MB/s | 2.1 MB     00:00
------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                 1.8 MB/s | 7.8 MB     00:04
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                              1/1
  Installing       : libXrender-0.9.10-16.el9.x86_64                                                                                             1/38
  Installing       : libXi-1.7.10-8.el9.x86_64                                                                                                   2/38
  Installing       : python3-setuptools-53.0.0-13.el9.noarch                                                                                     3/38
  Installing       : libnfsidmap-1:2.5.4-27.el9.x86_64                                                                                           4/38
  Installing       : python3-distro-1.5.0-7.el9.noarch                                                                                           5/38
  Installing       : python3-setools-4.4.4-1.el9.x86_64                                                                                          6/38
  Installing       : libXtst-1.2.3-16.el9.x86_64                                                                                                 7/38
  Installing       : libXrandr-1.5.2-8.el9.x86_64                                                                                                8/38
  Installing       : xorg-x11-xauth-1:1.1-10.el9.x86_64                                                                                          9/38
  Installing       : python3-audit-3.1.5-1.el9.x86_64                                                                                           10/38
  Installing       : libdmx-1.1.4-12.el9.x86_64                                                                                                 11/38
  Installing       : libXxf86vm-1.1.4-18.el9.x86_64                                                                                             12/38
  Installing       : libXxf86dga-1.1.5-8.el9.x86_64                                                                                             13/38
  Installing       : libXv-1.0.11-16.el9.x86_64                                                                                                 14/38
  Installing       : libXinerama-1.1.4-10.el9.x86_64                                                                                            15/38
  Installing       : libXcomposite-0.4.5-7.el9.x86_64                                                                                           16/38
  Installing       : libX11-xcb-1.7.0-9.el9.x86_64                                                                                              17/38
  Installing       : xorg-x11-utils-7.5-40.el9.x86_64                                                                                           18/38
  Installing       : ksh-3:1.0.6-3.el9.x86_64                                                                                                   19/38
  Running scriptlet: ksh-3:1.0.6-3.el9.x86_64                                                                                                   19/38
  Installing       : smartmontools-1:7.2-9.el9.x86_64                                                                                           20/38
  Running scriptlet: smartmontools-1:7.2-9.el9.x86_64                                                                                           20/38
Created symlink /etc/systemd/system/multi-user.target.wants/smartd.service → /usr/lib/systemd/system/smartd.service.

  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                                                                                                 21/38
  Installing       : rpcbind-1.2.6-7.el9.x86_64                                                                                                 21/38
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                                                                                                 21/38
Created symlink /etc/systemd/system/multi-user.target.wants/rpcbind.service → /usr/lib/systemd/system/rpcbind.service.
Created symlink /etc/systemd/system/sockets.target.wants/rpcbind.socket → /usr/lib/systemd/system/rpcbind.socket.

  Installing       : quota-nls-1:4.09-2.el9.noarch                                                                                              22/38
  Installing       : quota-1:4.09-2.el9.x86_64                                                                                                  23/38
  Installing       : python3-pyyaml-5.4.1-6.el9.x86_64                                                                                          24/38
  Installing       : python3-libsemanage-3.6-1.el9.x86_64                                                                                       25/38
  Installing       : libnsl-2.34-120.el9.x86_64                                                                                                 26/38
  Installing       : libev-4.33-5.el9.x86_64                                                                                                    27/38
  Installing       : libverto-libev-0.3.2-3.el9.x86_64                                                                                          28/38
  Installing       : gssproxy-0.8.4-7.el9.x86_64                                                                                                29/38
  Running scriptlet: gssproxy-0.8.4-7.el9.x86_64                                                                                                29/38
  Running scriptlet: nfs-utils-1:2.5.4-27.el9.x86_64                                                                                            30/38
  Installing       : nfs-utils-1:2.5.4-27.el9.x86_64                                                                                            30/38
  Running scriptlet: nfs-utils-1:2.5.4-27.el9.x86_64                                                                                            30/38
  Installing       : chkconfig-1.24-1.el9.x86_64                                                                                                31/38
  Installing       : initscripts-10.11.7-1.el9.x86_64                                                                                           32/38
  Running scriptlet: initscripts-10.11.7-1.el9.x86_64                                                                                           32/38
Created symlink /etc/systemd/system/sysinit.target.wants/import-state.service → /usr/lib/systemd/system/import-state.service.
Created symlink /etc/systemd/system/sysinit.target.wants/loadmodules.service → /usr/lib/systemd/system/loadmodules.service.

  Installing       : checkpolicy-3.6-1.el9.x86_64                                                                                               33/38
  Installing       : python3-policycoreutils-3.6-2.1.el9.noarch                                                                                 34/38
  Installing       : policycoreutils-python-utils-3.6-2.1.el9.noarch                                                                            35/38
  Installing       : bc-1.07.1-14.el9.x86_64                                                                                                    36/38
  Installing       : oracle-database-preinstall-21c-1.0-1.el8.x86_64                                                                            37/38
  Installing       : sssd-nfs-idmap-2.9.5-4.el9.x86_64                                                                                          38/38
  Running scriptlet: oracle-database-preinstall-21c-1.0-1.el8.x86_64                                                                            38/38
  Running scriptlet: sssd-nfs-idmap-2.9.5-4.el9.x86_64                                                                                          38/38
  Verifying        : bc-1.07.1-14.el9.x86_64                                                                                                     1/38
  Verifying        : checkpolicy-3.6-1.el9.x86_64                                                                                                2/38
  Verifying        : chkconfig-1.24-1.el9.x86_64                                                                                                 3/38
  Verifying        : gssproxy-0.8.4-7.el9.x86_64                                                                                                 4/38
  Verifying        : initscripts-10.11.7-1.el9.x86_64                                                                                            5/38
  Verifying        : libev-4.33-5.el9.x86_64                                                                                                     6/38
  Verifying        : libnfsidmap-1:2.5.4-27.el9.x86_64                                                                                           7/38
  Verifying        : libnsl-2.34-120.el9.x86_64                                                                                                  8/38
  Verifying        : libverto-libev-0.3.2-3.el9.x86_64                                                                                           9/38
  Verifying        : nfs-utils-1:2.5.4-27.el9.x86_64                                                                                            10/38
  Verifying        : python3-distro-1.5.0-7.el9.noarch                                                                                          11/38
  Verifying        : python3-libsemanage-3.6-1.el9.x86_64                                                                                       12/38
  Verifying        : python3-pyyaml-5.4.1-6.el9.x86_64                                                                                          13/38
  Verifying        : python3-setools-4.4.4-1.el9.x86_64                                                                                         14/38
  Verifying        : python3-setuptools-53.0.0-13.el9.noarch                                                                                    15/38
  Verifying        : quota-1:4.09-2.el9.x86_64                                                                                                  16/38
  Verifying        : quota-nls-1:4.09-2.el9.noarch                                                                                              17/38
  Verifying        : rpcbind-1.2.6-7.el9.x86_64                                                                                                 18/38
  Verifying        : smartmontools-1:7.2-9.el9.x86_64                                                                                           19/38
  Verifying        : sssd-nfs-idmap-2.9.5-4.el9.x86_64                                                                                          20/38
  Verifying        : ksh-3:1.0.6-3.el9.x86_64                                                                                                   21/38
  Verifying        : libX11-xcb-1.7.0-9.el9.x86_64                                                                                              22/38
  Verifying        : libXcomposite-0.4.5-7.el9.x86_64                                                                                           23/38
  Verifying        : libXi-1.7.10-8.el9.x86_64                                                                                                  24/38
  Verifying        : libXinerama-1.1.4-10.el9.x86_64                                                                                            25/38
  Verifying        : libXrandr-1.5.2-8.el9.x86_64                                                                                               26/38
  Verifying        : libXrender-0.9.10-16.el9.x86_64                                                                                            27/38
  Verifying        : libXtst-1.2.3-16.el9.x86_64                                                                                                28/38
  Verifying        : libXv-1.0.11-16.el9.x86_64                                                                                                 29/38
  Verifying        : libXxf86dga-1.1.5-8.el9.x86_64                                                                                             30/38
  Verifying        : libXxf86vm-1.1.4-18.el9.x86_64                                                                                             31/38
  Verifying        : libdmx-1.1.4-12.el9.x86_64                                                                                                 32/38
  Verifying        : policycoreutils-python-utils-3.6-2.1.el9.noarch                                                                            33/38
  Verifying        : python3-audit-3.1.5-1.el9.x86_64                                                                                           34/38
  Verifying        : python3-policycoreutils-3.6-2.1.el9.noarch                                                                                 35/38
  Verifying        : xorg-x11-utils-7.5-40.el9.x86_64                                                                                           36/38
  Verifying        : xorg-x11-xauth-1:1.1-10.el9.x86_64                                                                                         37/38
  Verifying        : oracle-database-preinstall-21c-1.0-1.el8.x86_64                                                                            38/38

Installed:
  bc-1.07.1-14.el9.x86_64                       checkpolicy-3.6-1.el9.x86_64                       chkconfig-1.24-1.el9.x86_64
  gssproxy-0.8.4-7.el9.x86_64                   initscripts-10.11.7-1.el9.x86_64                   ksh-3:1.0.6-3.el9.x86_64
  libX11-xcb-1.7.0-9.el9.x86_64                 libXcomposite-0.4.5-7.el9.x86_64                   libXi-1.7.10-8.el9.x86_64
  libXinerama-1.1.4-10.el9.x86_64               libXrandr-1.5.2-8.el9.x86_64                       libXrender-0.9.10-16.el9.x86_64
  libXtst-1.2.3-16.el9.x86_64                   libXv-1.0.11-16.el9.x86_64                         libXxf86dga-1.1.5-8.el9.x86_64
  libXxf86vm-1.1.4-18.el9.x86_64                libdmx-1.1.4-12.el9.x86_64                         libev-4.33-5.el9.x86_64
  libnfsidmap-1:2.5.4-27.el9.x86_64             libnsl-2.34-120.el9.x86_64                         libverto-libev-0.3.2-3.el9.x86_64
  nfs-utils-1:2.5.4-27.el9.x86_64               oracle-database-preinstall-21c-1.0-1.el8.x86_64    policycoreutils-python-utils-3.6-2.1.el9.noarch
  python3-audit-3.1.5-1.el9.x86_64              python3-distro-1.5.0-7.el9.noarch                  python3-libsemanage-3.6-1.el9.x86_64
  python3-policycoreutils-3.6-2.1.el9.noarch    python3-pyyaml-5.4.1-6.el9.x86_64                  python3-setools-4.4.4-1.el9.x86_64
  python3-setuptools-53.0.0-13.el9.noarch       quota-1:4.09-2.el9.x86_64                          quota-nls-1:4.09-2.el9.noarch
  rpcbind-1.2.6-7.el9.x86_64                    smartmontools-1:7.2-9.el9.x86_64                   sssd-nfs-idmap-2.9.5-4.el9.x86_64
  xorg-x11-utils-7.5-40.el9.x86_64              xorg-x11-xauth-1:1.1-10.el9.x86_64

Complete!
[root@centos9s distr]#dnf localinstall oracle-database-ee-21c-1.0-1.ol8.x86_64.rpm
Last metadata expiration check: 0:04:04 ago on Sat 24 Aug 2024 03:53:55 PM UTC.
Dependencies resolved.
======================================================================================================================================================
 Package                                       Architecture                  Version                        Repository                           Size
======================================================================================================================================================
Installing:
 oracle-database-ee-21c                        x86_64                        1.0-1                          @commandline                        2.6 G

Transaction Summary
======================================================================================================================================================
Install  1 Package

Total size: 2.6 G
Installed size: 7.1 G
Is this ok [y/N]: y
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                              1/1
  Running scriptlet: oracle-database-ee-21c-1.0-1.x86_64                                                                                          1/1
  Installing       : oracle-database-ee-21c-1.0-1.x86_64                                                                                          1/1
  Running scriptlet: oracle-database-ee-21c-1.0-1.x86_64                                                                                          1/1
[INFO] Executing post installation scripts...
[INFO] Oracle home installed successfully and ready to be configured.
To configure a sample Oracle Database you can execute the following service configuration script as root: /etc/init.d/oracledb_ORCLCDB-21c configure

  Verifying        : oracle-database-ee-21c-1.0-1.x86_64                                                                                          1/1

Installed:
  oracle-database-ee-21c-1.0-1.x86_64

Complete!
[root@centos9s distr]#


```

## Install PostgreSQL 16

```bash
[root@centos9s /]# dnf install postgresql-server
Extra Packages for Enterprise Linux 9 - x86_64                                                                         24 kB/s |  15 kB     00:00
Extra Packages for Enterprise Linux 9 - Next - x86_64                                                                  69 kB/s |  46 kB     00:00
Dependencies resolved.
======================================================================================================================================================
 Package                                       Architecture                 Version                             Repository                       Size
======================================================================================================================================================
Installing:
 postgresql-server                             x86_64                       13.16-1.el9                         appstream                       5.8 M
Installing dependencies:
 libicu                                        x86_64                       67.1-9.el9                          baseos                          9.6 M
 postgresql                                    x86_64                       13.16-1.el9                         appstream                       1.6 M
 postgresql-private-libs                       x86_64                       13.16-1.el9                         appstream                       137 k

Transaction Summary
======================================================================================================================================================
Install  4 Packages

Total download size: 17 M
Installed size: 62 M
Is this ok [y/N]: y
Downloading Packages:
(1/4): postgresql-13.16-1.el9.x86_64.rpm                                                                              1.8 MB/s | 1.6 MB     00:00
(2/4): postgresql-private-libs-13.16-1.el9.x86_64.rpm                                                                 101 kB/s | 137 kB     00:01
(3/4): postgresql-server-13.16-1.el9.x86_64.rpm                                                                       3.4 MB/s | 5.8 MB     00:01
(4/4): libicu-67.1-9.el9.x86_64.rpm                                                                                   2.3 MB/s | 9.6 MB     00:04
------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                 3.2 MB/s |  17 MB     00:05
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                              1/1
  Installing       : postgresql-private-libs-13.16-1.el9.x86_64                                                                                   1/4
  Installing       : postgresql-13.16-1.el9.x86_64                                                                                                2/4
  Installing       : libicu-67.1-9.el9.x86_64                                                                                                     3/4
  Running scriptlet: postgresql-server-13.16-1.el9.x86_64                                                                                         4/4
  Installing       : postgresql-server-13.16-1.el9.x86_64                                                                                         4/4
  Running scriptlet: postgresql-server-13.16-1.el9.x86_64                                                                                         4/4
  Verifying        : libicu-67.1-9.el9.x86_64                                                                                                     1/4
  Verifying        : postgresql-13.16-1.el9.x86_64                                                                                                2/4
  Verifying        : postgresql-private-libs-13.16-1.el9.x86_64                                                                                   3/4
  Verifying        : postgresql-server-13.16-1.el9.x86_64                                                                                         4/4

Installed:
  libicu-67.1-9.el9.x86_64    postgresql-13.16-1.el9.x86_64    postgresql-private-libs-13.16-1.el9.x86_64    postgresql-server-13.16-1.el9.x86_64

Complete!
[root@centos9s /]# 
```

### Post Install

```bash
#service postgresql initdb
#chkconfig postgresql on
initdb -D /u01/pgdata/
pg_ctl start -D /u01/pgdata -l logfile
```

## Load test data in Oracle

```sql
alter pluggable database pdb1 open;
alter pluggable database pdb1 save state;

create user scott identified by tiger;
grant connect, resource to scott;
alter user scott quota unlimited on users;

create table scott.clients (client_id number(2) not null, firstname varchar2(100) not null, lastname varchar2(100) not null, PRIMARY KEY (client_id));
create table scott.services (service_id number(2) not null, servname varchar2(100) not null, PRIMARY KEY (service_id));
create table scott.payments (pmnt_id number(4) not null, client_id number(2) not null, service_id number(2) not null, period number(6) not null, amount number(10) not null, data date default sysdate, PRIMARY KEY (pmnt_id));
create table scott.charges (chg_id number(4) not null, client_id number(2) not null, service_id number(2) not null, period number(6) not null, amount number(10) not null, data date default sysdate, PRIMARY KEY (chg_id));

alter table scott.payments add constraint pmnt_cl_fk foreign key(client_id) references scott.clients(client_id);
alter table scott.payments add constraint pmnt_srv_fk foreign key(service_id) references scott.services(service_id);
alter table scott.charges add constraint chg_cl_fk foreign key(client_id) references scott.clients(client_id);
alter table scott.charges add constraint vhg_srv_fk foreign key(service_id) references scott.services(service_id);

insert into scott.clients(client_id, firstname, lastname) values (1, 'Кирилл', 'Иванов');
insert into scott.clients(client_id, firstname, lastname) values (2, 'Павел', 'Ветров');
insert into scott.clients(client_id, firstname, lastname) values (3, 'Иван', 'Сидоров');
insert into scott.clients(client_id, firstname, lastname) values (4, 'Артём', 'Солнцев');
insert into scott.clients(client_id, firstname, lastname) values (5, 'Ирина', 'Авдеева');

insert into scott.services(service_id, servname) values (1, 'Электроэнергия');
insert into scott.services(service_id, servname) values (2, 'Газоснабжение');
insert into scott.services(service_id, servname) values (3, 'ХВС');
insert into scott.services(service_id, servname) values (4, 'ГВС');

insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(1,1,1,202401,393688);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(2,1,2,202401,535262);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(3,1,3,202401,252111);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(4,1,4,202401,549400);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(5,2,1,202401,291387);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(6,2,2,202401,121710);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(7,2,3,202401,251687);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(8,2,4,202401,234442);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(9,3,1,202401,127024);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(10,3,2,202401,98551);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(11,3,3,202401,142665);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(12,3,4,202401,38300);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(13,4,1,202401,194238);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(14,4,2,202401,25908);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(15,4,3,202401,51409);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(16,4,4,202401,211553);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(17,5,1,202401,558190);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(18,5,2,202401,73086);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(19,5,3,202401,113265);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(20,5,4,202401,119883);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(21,1,1,202402,179165);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(22,1,2,202402,215382);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(23,1,3,202402,71226);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(24,1,4,202402,52900);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(25,2,1,202402,393210);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(26,2,2,202402,156507);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(27,2,3,202402,157640);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(28,2,4,202402,63298);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(29,3,1,202402,40398);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(30,3,2,202402,17956);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(31,3,3,202402,231604);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(32,3,4,202402,462956);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(33,4,1,202402,232677);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(34,4,2,202402,143458);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(35,4,3,202402,254717);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(36,4,4,202402,236280);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(37,5,1,202402,47384);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(38,5,2,202402,187564);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(39,5,3,202402,199996);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(40,5,4,202402,191467);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(41,1,1,202403,153511);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(42,1,2,202403,563614);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(43,1,3,202403,154496);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(44,1,4,202403,80226);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(45,2,1,202403,24180);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(46,2,2,202403,343730);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(47,2,3,202403,275515);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(48,2,4,202403,41773);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(49,3,1,202403,45739);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(50,3,2,202403,17296);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(51,3,3,202403,68541);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(52,3,4,202403,384434);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(53,4,1,202403,123170);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(54,4,2,202403,12325);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(55,4,3,202403,259238);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(56,4,4,202403,102227);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(57,5,1,202403,39963);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(58,5,2,202403,134616);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(59,5,3,202403,244556);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(60,5,4,202403,207876);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(61,1,1,202404,481696);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(62,1,2,202404,64905);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(63,1,3,202404,261908);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(64,1,4,202404,232780);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(65,2,1,202404,26320);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(66,2,2,202404,100256);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(67,2,3,202404,275532);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(68,2,4,202404,57968);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(69,3,1,202404,137822);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(70,3,2,202404,100753);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(71,3,3,202404,156903);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(72,3,4,202404,176722);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(73,4,1,202404,28983);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(74,4,2,202404,34494);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(75,4,3,202404,400334);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(76,4,4,202404,199721);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(77,5,1,202404,43758);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(78,5,2,202404,235874);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(79,5,3,202404,224269);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(80,5,4,202404,63588);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(81,1,1,202405,25199);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(82,1,2,202405,34538);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(83,1,3,202405,343718);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(84,1,4,202405,176656);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(85,2,1,202405,264023);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(86,2,2,202405,268814);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(87,2,3,202405,275766);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(88,2,4,202405,104226);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(89,3,1,202405,127990);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(90,3,2,202405,116280);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(91,3,3,202405,165533);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(92,3,4,202405,18549);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(93,4,1,202405,320624);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(94,4,2,202405,114944);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(95,4,3,202405,100454);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(96,4,4,202405,288648);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(97,5,1,202405,25805);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(98,5,2,202405,60557);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(99,5,3,202405,91417);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(100,5,4,202405,252524);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(101,1,1,202406,66839);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(102,1,2,202406,63863);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(103,1,3,202406,30736);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(104,1,4,202406,24300);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(105,2,1,202406,135711);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(106,2,2,202406,572334);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(107,2,3,202406,35079);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(108,2,4,202406,136708);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(109,3,1,202406,254618);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(110,3,2,202406,31144);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(111,3,3,202406,125499);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(112,3,4,202406,223842);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(113,4,1,202406,44533);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(114,4,2,202406,68948);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(115,4,3,202406,179067);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(116,4,4,202406,130514);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(117,5,1,202406,92616);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(118,5,2,202406,182021);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(119,5,3,202406,64297);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(120,5,4,202406,424842);

insert into scott.charges (chg_id, client_id, service_id, period, amount) values(1,1,1,202401,196844);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(2,1,2,202401,267631);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(3,1,3,202401,252111);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(4,1,4,202401,274700);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(5,2,1,202401,291387);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(6,2,2,202401,60855);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(7,2,3,202401,251687);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(8,2,4,202401,234442);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(9,3,1,202401,254048);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(10,3,2,202401,98551);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(11,3,3,202401,285330);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(12,3,4,202401,76600);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(13,4,1,202401,194238);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(14,4,2,202401,51815);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(15,4,3,202401,102817);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(16,4,4,202401,211553);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(17,5,1,202401,279095);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(18,5,2,202401,146172);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(19,5,3,202401,226530);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(20,5,4,202401,119883);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(21,1,1,202402,179165);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(22,1,2,202402,215382);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(23,1,3,202402,142452);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(24,1,4,202402,105799);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(25,2,1,202402,196605);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(26,2,2,202402,156507);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(27,2,3,202402,157640);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(28,2,4,202402,63298);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(29,3,1,202402,80795);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(30,3,2,202402,17956);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(31,3,3,202402,115802);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(32,3,4,202402,231478);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(33,4,1,202402,232677);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(34,4,2,202402,286915);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(35,4,3,202402,254717);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(36,4,4,202402,118140);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(37,5,1,202402,47384);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(38,5,2,202402,187564);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(39,5,3,202402,99998);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(40,5,4,202402,191467);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(41,1,1,202403,153511);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(42,1,2,202403,281807);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(43,1,3,202403,154496);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(44,1,4,202403,160451);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(45,2,1,202403,48359);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(46,2,2,202403,171865);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(47,2,3,202403,275515);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(48,2,4,202403,41773);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(49,3,1,202403,45739);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(50,3,2,202403,34592);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(51,3,3,202403,68541);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(52,3,4,202403,192217);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(53,4,1,202403,61585);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(54,4,2,202403,12325);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(55,4,3,202403,129619);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(56,4,4,202403,204454);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(57,5,1,202403,79926);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(58,5,2,202403,269231);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(59,5,3,202403,244556);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(60,5,4,202403,103938);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(61,1,1,202404,240848);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(62,1,2,202404,129809);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(63,1,3,202404,130954);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(64,1,4,202404,232780);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(65,2,1,202404,52639);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(66,2,2,202404,200512);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(67,2,3,202404,137766);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(68,2,4,202404,115935);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(69,3,1,202404,275643);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(70,3,2,202404,201506);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(71,3,3,202404,156903);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(72,3,4,202404,176722);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(73,4,1,202404,28983);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(74,4,2,202404,34494);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(75,4,3,202404,200167);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(76,4,4,202404,199721);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(77,5,1,202404,21879);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(78,5,2,202404,235874);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(79,5,3,202404,224269);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(80,5,4,202404,31794);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(81,1,1,202405,25199);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(82,1,2,202405,69075);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(83,1,3,202405,171859);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(84,1,4,202405,176656);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(85,2,1,202405,264023);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(86,2,2,202405,268814);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(87,2,3,202405,137883);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(88,2,4,202405,104226);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(89,3,1,202405,127990);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(90,3,2,202405,116280);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(91,3,3,202405,165533);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(92,3,4,202405,18549);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(93,4,1,202405,160312);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(94,4,2,202405,229888);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(95,4,3,202405,100454);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(96,4,4,202405,144324);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(97,5,1,202405,25805);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(98,5,2,202405,60557);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(99,5,3,202405,182833);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(100,5,4,202405,252524);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(101,1,1,202406,133678);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(102,1,2,202406,127726);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(103,1,3,202406,30736);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(104,1,4,202406,48600);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(105,2,1,202406,271421);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(106,2,2,202406,286167);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(107,2,3,202406,35079);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(108,2,4,202406,273416);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(109,3,1,202406,254618);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(110,3,2,202406,31144);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(111,3,3,202406,125499);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(112,3,4,202406,223842);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(113,4,1,202406,89065);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(114,4,2,202406,68948);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(115,4,3,202406,179067);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(116,4,4,202406,130514);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(117,5,1,202406,185231);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(118,5,2,202406,182021);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(119,5,3,202406,64297);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(120,5,4,202406,212421);

commit;
```

