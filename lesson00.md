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
exit

