# TP 1 Maîtrise de poste

## Self-footprinting

### Host OS

nom de la machine

```
PS C:\Users\Mathieu> Get-ComputerInfo
CsCaption                                               : LAPTOP-J893675Q
```

OS et version

```
PS C:\Users\Mathieu> Get-ComputerInfo
WindowsProductName                                      : Windows 10 Home
WindowsVersion                                          : 1909
```

architecture processeur (32-bit, 64-bit, ARM, etc)

```
PS C:\Users\Mathieu> Get-ComputerInfo
CsSystemType                                            : x64-based PC
```

modèle du processeur

```
PS C:\Users\Mathieu> Get-ComputerInfo

Processors                                            : {Intel(R) Core(TM) i7-8750H CPU @ 2.20GHz}
```

Le nom de mon processeur (Intel(R) Core(TM) i7-8750H) est composé de sa marque, Intel(R) Core(TM), le i7 et là pour indiqué un "type" de processeur (référence pour la marque et le consommateur), le premier chiffre après le i7 et pour la génération du processeur, les 3 chiffres après sont les SKU (Stock Keeping Unit) c'est à dire le numéro du modèle, le U veut dire que le processeur est un ultra-low power c'est à dire qu'il ne prend pas beaucoup de batterie.
quantité RAM et modèle de la RAM

```
PS C:\Users\Mathieu> Get-WmiObject win32_physicalmemory | Format-Table Manufacturer,Banklabel,Configuredclockspeed,Devicelocator,Capacity,Serialnumber -autosize

Manufacturer Banklabel Configuredclockspeed Devicelocator    Capacity Serialnumber
------------ --------- -------------------- -------------    -------- ------------
SK Hynix     BANK 0                    2667 ChannelA-DIMM0 8589934592 529770E9
```

### Devices

la marque et le modèle de mon processeur

```
Intel(R) Core(TM) i7-8750H CPU @ 2.20GHz
```

```
PS C:\Users\Mathieu> WMIC CPU Get DeviceID,NumberOfCores,NumberOfLogicalProcessors
DeviceID  NumberOfCores  NumberOfLogicalProcessors
CPU0      6              12
```

ou alors :

```
PS C:\Users\Mathieu> echo $env:NUMBER_OF_PROCESSORS
12
```

La lettre H veut dire Haswell qui correspond à la microarchitecture x86-64

Disque dur

```
PS C:\Users\Mathieu> Get-PhysicalDisk

Number FriendlyName               SerialNumber                   MediaType CanPool OperationalStatus HealthStatus Usage            Size
------ ------------               ------------                   --------- ------- ----------------- ------------ -----            ----
1      KINGSTON RBUSNS8154P3128GJ 50026B76821DC92A    _00000001. SSD       False   OK                Healthy      Auto-Select 119.24 GB
0      TOSHIBA MQ04ABF100         984CP8FWT                      HDD       False   OK                Healthy      Auto-Select 931.51 GB
```

Partition

```
PS C:\Users\Mathieu> Get-Partition


   DiskPath : \\?\scsi#disk&ven_nvme&prod_kingston_rbusns8#4&1f9bbd7e&0&010000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                                                                                   Size Type
---------------  ----------- ------                                                                                                   ---- ----
1                            1048576                                                                                                260 MB System
2                            273678336                                                                                               16 MB Reserved
3                C           290455552                                                                                           118.19 GB Basic
4                            127196463104                                                                                           800 MB Recovery


   DiskPath : \\?\scsi#disk&ven_toshiba&prod_mq04abf100#4&1f9bbd7e&0&000400#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                                                                                   Size Type
---------------  ----------- ------                                                                                                   ---- ----
1                D           1048576                                                                                             931.51 GB Basic
```

System : Cette partition contient les fichiers de boot de l'ordinateur.

Reserved : Cette partition contient les fichiers essentiel à l'ordinateur.

Basic : Cette partition contient l'OS de l'ordinateur.

Recovery : Cette partition contient les fichiers et dossier de récupération en cas de problème.

### NETWORK

On va lister les cartes réseaux grâce a la commande `Get-NetAdapter | fl Name, InterfaceIndex`

```
Name           : VMware Network Adapter VMnet1
InterfaceIndex : 25

Name           : Ethernet
InterfaceIndex : 24

Name           : VirtualBox Host-Only Network #2
InterfaceIndex : 20

Name           : VirtualBox Host-Only Network
InterfaceIndex : 19

Name           : Npcap Loopback Adapter
InterfaceIndex : 16

Name           : VirtualBox Host-Only Network #3
InterfaceIndex : 15

Name           : VMware Network Adapter VMnet8
InterfaceIndex : 7

Name           : Connexion réseau Bluetooth
InterfaceIndex : 6

Name           : Wi-Fi
InterfaceIndex : 4
```

On liste les ports TCP et UDP

```
PS C:\Users\Mathieu> netstat -an

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    0.0.0.0:80             0.0.0.0:0              LISTENING
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING
  TCP    0.0.0.0:902            0.0.0.0:0              LISTENING
  TCP    0.0.0.0:912            0.0.0.0:0              LISTENING
  TCP    0.0.0.0:3306           0.0.0.0:0              LISTENING
  TCP    0.0.0.0:5040           0.0.0.0:0              LISTENING
  TCP    0.0.0.0:6646           0.0.0.0:0              LISTENING
  TCP    0.0.0.0:7680           0.0.0.0:0              LISTENING
  TCP    0.0.0.0:33060          0.0.0.0:0              LISTENING
  TCP    0.0.0.0:49664          0.0.0.0:0              LISTENING
  TCP    0.0.0.0:49665          0.0.0.0:0              LISTENING
  TCP    0.0.0.0:49666          0.0.0.0:0              LISTENING
  TCP    0.0.0.0:49667          0.0.0.0:0              LISTENING
  TCP    0.0.0.0:49668          0.0.0.0:0              LISTENING
  TCP    0.0.0.0:49670          0.0.0.0:0              LISTENING
  TCP    0.0.0.0:49678          0.0.0.0:0              LISTENING
  TCP    10.3.1.1:139           0.0.0.0:0              LISTENING
  TCP    10.3.2.1:139           0.0.0.0:0              LISTENING
  TCP    10.4.1.1:139           0.0.0.0:0              LISTENING
  TCP    127.0.0.1:2992         0.0.0.0:0              LISTENING
  TCP    127.0.0.1:5939         0.0.0.0:0              LISTENING
  TCP    127.0.0.1:6463         0.0.0.0:0              LISTENING
  TCP    127.0.0.1:49686        127.0.0.1:49687        ESTABLISHED
  TCP    127.0.0.1:49687        127.0.0.1:49686        ESTABLISHED
  TCP    127.0.0.1:54426        0.0.0.0:0              LISTENING
  TCP    169.254.194.12:139     0.0.0.0:0              LISTENING
  TCP    192.168.1.45:139       0.0.0.0:0              LISTENING
  TCP    192.168.1.45:2823      216.59.56.23:443       ESTABLISHED
  TCP    192.168.1.45:2825      216.59.56.23:443       ESTABLISHED
  TCP    192.168.1.45:2826      216.59.56.23:443       ESTABLISHED
  TCP    192.168.1.45:3013      52.236.190.6:443       ESTABLISHED
  TCP    192.168.1.45:4054      162.159.135.234:443    ESTABLISHED
  TCP    192.168.1.45:4090      188.65.124.58:443      ESTABLISHED
  TCP    192.168.1.45:4093      140.82.114.26:443      ESTABLISHED
  TCP    192.168.1.45:4094      140.82.114.26:443      ESTABLISHED
  TCP    192.168.1.45:4103      162.159.134.233:443    ESTABLISHED
  TCP    192.168.1.45:4106      52.157.234.37:443      ESTABLISHED
  TCP    192.168.1.45:49857     40.67.254.36:443       ESTABLISHED
  TCP    192.168.1.45:50120     162.159.137.234:443    ESTABLISHED
  TCP    192.168.78.1:139       0.0.0.0:0              LISTENING
  TCP    192.168.178.1:139      0.0.0.0:0              LISTENING
  TCP    [::]:80                [::]:0                 LISTENING
  TCP    [::]:135               [::]:0                 LISTENING
  TCP    [::]:445               [::]:0                 LISTENING
  TCP    [::]:3306              [::]:0                 LISTENING
  TCP    [::]:7680              [::]:0                 LISTENING
  TCP    [::]:33060             [::]:0                 LISTENING
  TCP    [::]:49664             [::]:0                 LISTENING
  TCP    [::]:49665             [::]:0                 LISTENING
  TCP    [::]:49666             [::]:0                 LISTENING
  TCP    [::]:49667             [::]:0                 LISTENING
  TCP    [::]:49668             [::]:0                 LISTENING
  TCP    [::]:49670             [::]:0                 LISTENING
  TCP    [::]:49678             [::]:0                 LISTENING
  TCP    [::1]:49723            [::]:0                 LISTENING
  TCP    [2a01:cb19:944:7500:fc07:3709:bb02:331e]:49963  [2a02:26f0:e3:3aa::57]:443  CLOSE_WAIT
  TCP    [2a01:cb19:944:7500:fc07:3709:bb02:331e]:50047  [2a00:1450:400c:c0b::bc]:5228  ESTABLISHED
  UDP    0.0.0.0:500            *:*
  UDP    0.0.0.0:3702           *:*
  UDP    0.0.0.0:3702           *:*
  UDP    0.0.0.0:4500           *:*
  UDP    0.0.0.0:5050           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5353           *:*
  UDP    0.0.0.0:5355           *:*
  UDP    0.0.0.0:6646           *:*
  UDP    0.0.0.0:57305          *:*
  UDP    0.0.0.0:62149          *:*
  UDP    0.0.0.0:63081          *:*
  UDP    10.3.1.1:137           *:*
  UDP    10.3.1.1:138           *:*
  UDP    10.3.1.1:1900          *:*
  UDP    10.3.1.1:2177          *:*
  UDP    10.3.1.1:5353          *:*
  UDP    10.3.1.1:55813         *:*
  UDP    10.3.2.1:137           *:*
  UDP    10.3.2.1:138           *:*
  UDP    10.3.2.1:1900          *:*
  UDP    10.3.2.1:2177          *:*
  UDP    10.3.2.1:5353          *:*
  UDP    10.3.2.1:55815         *:*
  UDP    10.4.1.1:137           *:*
  UDP    10.4.1.1:138           *:*
  UDP    10.4.1.1:1900          *:*
  UDP    10.4.1.1:2177          *:*
  UDP    10.4.1.1:5353          *:*
  UDP    10.4.1.1:55816         *:*
  UDP    127.0.0.1:1900         *:*
  UDP    127.0.0.1:55820        *:*
  UDP    127.0.0.1:64508        *:*
  UDP    169.254.62.122:5353    *:*
  UDP    169.254.194.12:137     *:*
  UDP    169.254.194.12:138     *:*
  UDP    169.254.194.12:1900    *:*
  UDP    169.254.194.12:2177    *:*
  UDP    169.254.194.12:5353    *:*
  UDP    169.254.194.12:55814   *:*
  UDP    169.254.198.210:5353   *:*
  UDP    192.168.1.45:137       *:*
  UDP    192.168.1.45:138       *:*
  UDP    192.168.1.45:1900      *:*
  UDP    192.168.1.45:2177      *:*
  UDP    192.168.1.45:5353      *:*
  UDP    192.168.1.45:55819     *:*
  UDP    192.168.78.1:137       *:*
  UDP    192.168.78.1:138       *:*
  UDP    192.168.78.1:1900      *:*
  UDP    192.168.78.1:2177      *:*
  UDP    192.168.78.1:55817     *:*
  UDP    192.168.178.1:137      *:*
  UDP    192.168.178.1:138      *:*
  UDP    192.168.178.1:1900     *:*
  UDP    192.168.178.1:2177     *:*
  UDP    192.168.178.1:55818    *:*
  UDP    [::]:500               *:*
  UDP    [::]:3702              *:*
  UDP    [::]:3702              *:*
  UDP    [::]:4500              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5353              *:*
  UDP    [::]:5355              *:*
  UDP    [::]:57305             *:*
  UDP    [::]:63082             *:*
  UDP    [::1]:1900             *:*
  UDP    [::1]:55812            *:*
  UDP    [2a01:cb19:944:7500:29ef:37fb:424d:e91f]:2177  *:*
  UDP    [2a01:cb19:944:7500:fc07:3709:bb02:331e]:2177  *:*
  UDP    [fe80::217e:cd0f:4c2e:e97d%19]:1900  *:*
  UDP    [fe80::217e:cd0f:4c2e:e97d%19]:2177  *:*
  UDP    [fe80::217e:cd0f:4c2e:e97d%19]:55805  *:*
  UDP    [fe80::29ef:37fb:424d:e91f%4]:1900  *:*
  UDP    [fe80::29ef:37fb:424d:e91f%4]:2177  *:*
  UDP    [fe80::29ef:37fb:424d:e91f%4]:55811  *:*
  UDP    [fe80::4de8:fc0f:257f:3e7a%7]:1900  *:*
  UDP    [fe80::4de8:fc0f:257f:3e7a%7]:2177  *:*
  UDP    [fe80::4de8:fc0f:257f:3e7a%7]:5353  *:*
  UDP    [fe80::4de8:fc0f:257f:3e7a%7]:55810  *:*
  UDP    [fe80::5061:5302:5bd4:4539%15]:1900  *:*
  UDP    [fe80::5061:5302:5bd4:4539%15]:2177  *:*
  UDP    [fe80::5061:5302:5bd4:4539%15]:55808  *:*
  UDP    [fe80::b50d:14d:6633:c20c%16]:1900  *:*
  UDP    [fe80::b50d:14d:6633:c20c%16]:2177  *:*
  UDP    [fe80::b50d:14d:6633:c20c%16]:5353  *:*
  UDP    [fe80::b50d:14d:6633:c20c%16]:55806  *:*
  UDP    [fe80::e8f8:abe1:41e4:f117%20]:1900  *:*
  UDP    [fe80::e8f8:abe1:41e4:f117%20]:2177  *:*
  UDP    [fe80::e8f8:abe1:41e4:f117%20]:55807  *:*
  UDP    [fe80::fdd4:ecfe:4bc9:c6d2%25]:1900  *:*
  UDP    [fe80::fdd4:ecfe:4bc9:c6d2%25]:2177  *:*
  UDP    [fe80::fdd4:ecfe:4bc9:c6d2%25]:5353  *:*
  UDP    [fe80::fdd4:ecfe:4bc9:c6d2%25]:55809  *:*
```

- déterminer quel programme tourne derrière chacun des ports

```
PS C:\Users\Mathieu> Get-Process | Where-Object {$_.mainWindowTitle} | Format-Table Id, Name, mainWindowtitle -AutoSize

   Id Name                                                           MainWindowTitle
   -- ----                                                           ---------------
22140 ApplicationFrameHost                                           Calculatrice
14920 Calculator                                                     Calculatrice
 8684 chrome                                                         Ynov - Extranet - Google Chrome
18988 Code                                                           ● tp1.md - Visual Studio Code
 9644 CodeSetup-stable-d69a79b73808559a91206d73d7717ff5f798f23c.tmp  Installation
21312 Discord                                                        #📑-cour - Discord
15300 MicrosoftEdge                                                  Microsoft Edge
23740 MicrosoftEdgeCP                                                Microsoft Edge
12956 powershell                                                     Windows PowerShell
24324 SystemSettings                                                 CN=Microsoft Windows, O=Microsoft Corporation, ...
24108 WindowsInternal.ComposableShell.Experiences.TextInput.InputApp Microsoft Text Input Application
```

- expliquer la fonction de chacun de ces programmes

`15300 MicrosoftEdge Microsoft Edge`
MicrosoftEdge est un navigateur web qui tourne au port 15300 en UDP

### User

On va lister les utilisateurs présent ce PC avec la commande `net user` :

```
PS C:\Users\Mathieu> net user

comptes d’utilisateurs de \\LAPTOP-J893675Q

-------------------------------------------------------------------------------
Administrateur           DefaultAccount           Invité
Mathieu                  SQLEXPRESS01             SQLEXPRESS02
SQLEXPRESS03             SQLEXPRESS04             SQLEXPRESS05
SQLEXPRESS06             SQLEXPRESS07             SQLEXPRESS08
SQLEXPRESS09             SQLEXPRESS10             SQLEXPRESS11
SQLEXPRESS12             SQLEXPRESS13             SQLEXPRESS14
SQLEXPRESS15             SQLEXPRESS16             SQLEXPRESS17
SQLEXPRESS18             SQLEXPRESS19             SQLEXPRESS20
WDAGUtilityAccount       YNOV01                   YNOV02
YNOV03                   YNOV04                   YNOV05
YNOV06                   YNOV07                   YNOV08
YNOV09                   YNOV10                   YNOV11
YNOV12                   YNOV13                   YNOV14
YNOV15                   YNOV16                   YNOV17
YNOV18                   YNOV19                   YNOV20
La commande s’est terminée correctement.
```

Déterminer le nom de l'utilisateur qui est full admin sur la machine

```
PS C:\Users\Mathieu> Get-LocalUser

Name               Enabled Description
----               ------- -----------
Administrateur     False   Compte d’utilisateur d’administration
Mathieu            True
```

### Processus

Pour lister tout les processus en arrière plan avec la commande `tasklist` :

On va pas tout mettre sinon ce sera illisible :

```
PS C:\Users\Mathieu> tasklist

Nom de l’image                 PID Nom de la sessio Numéro de s Utilisation
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0         8 Ko
System                           4 Services                   0       128 Ko
Registry                       144 Services                   0    85 904 Ko
smss.exe                      1008 Services                   0       952 Ko
csrss.exe                      680 Services                   0     3 508 Ko
wininit.exe                    920 Services                   0     3 204 Ko
csrss.exe                      932 Console                    1     4 040 Ko
services.exe                   116 Services                   0     7 716 Ko
winlogon.exe                   120 Console                    1     8 160 Ko
lsass.exe                      660 Services                   0    14 380 Ko
svchost.exe                   1080 Services                   0     2 104 Ko
svchost.exe                   1128 Services                   0    28 164 Ko
fontdrvhost.exe               1152 Console                    1     3 548 Ko
fontdrvhost.exe               1160 Services                   0     1 692 Ko
WUDFHost.exe                  1168 Services                   0    11 192 Ko
svchost.exe                   1288 Services                   0    15 660 Ko
WUDFHost.exe                  1352 Services                   0     4 368 Ko
svchost.exe                   1380 Services                   0     6 440 Ko
dwm.exe                       1504 Console                    1    65 596 Ko
svchost.exe                   1588 Services                   0     6 120 Ko
svchost.exe                   1628 Services                   0     8 044 Ko
svchost.exe                   1636 Services                   0     7 708 Ko
svchost.exe                   1644 Services                   0     4 728 Ko
svchost.exe                   1756 Services                   0     7 620 Ko
svchost.exe                   1876 Services                   0     9 140 Ko
svchost.exe                   1964 Services                   0     5 668 Ko
svchost.exe                   1984 Services                   0    12 508 Ko
svchost.exe                   2004 Services                   0     3 588 Ko
svchost.exe                    860 Services                   0     4 684 Ko
svchost.exe                   1460 Services                   0     8 732 Ko
svchost.exe                   2088 Services                   0     3 536 Ko
svchost.exe                   2144 Services                   0    12 616 Ko
svchost.exe                   2188 Services                   0     5 368 Ko
svchost.exe                   2340 Services                   0     5 424 Ko
svchost.exe                   2408 Services                   0     7 948 Ko
svchost.exe                   2448 Services                   0     4 020 Ko
igfxCUIService.exe            2560 Services                   0     5 464 Ko
svchost.exe                   2584 Services                   0    12 612 Ko
svchost.exe                   2604 Services                   0     7 748 Ko
svchost.exe                   2696 Services                   0     7 760 Ko
svchost.exe                   2772 Services                   0     5 124 Ko
svchost.exe                   2780 Services                   0     5 840 Ko
svchost.exe                   2796 Services                   0     3 812 Ko
NVDisplay.Container.exe       2804 Services                   0    10 088 Ko
svchost.exe                   2900 Services                   0    13 236 Ko
svchost.exe                   2960 Services                   0     4 972 Ko
dasHost.exe                   3012 Services                   0     6 340 Ko
svchost.exe                   1480 Services                   0     7 188 Ko
svchost.exe                   3076 Services                   0    10 704 Ko
svchost.exe                   3084 Services                   0     3 356 Ko
svchost.exe                   3092 Services                   0     5 060 Ko
svchost.exe                   3116 Services                   0    10 080 Ko
svchost.exe                   3224 Services                   0     4 536 Ko
svchost.exe                   3232 Services                   0     4 544 Ko
Memory Compression            3280 Services                   0   597 896 Ko
svchost.exe                   3512 Services                   0     6 956 Ko
NVDisplay.Container.exe       3672 Console                    1    17 840 Ko
svchost.exe                   3708 Services                   0    11 684 Ko
svchost.exe                   3996 Services                   0     6 956 Ko
svchost.exe                   4004 Services                   0     4 236 Ko
svchost.exe                   3780 Services                   0     5 116 Ko
svchost.exe                   4164 Services                   0    15 096 Ko
svchost.exe                   4228 Services                   0     9 520 Ko
AsLdrSrv64.exe                4236 Services                   0     3 548 Ko
spoolsv.exe                   4404 Services                   0    16 976 Ko
svchost.exe                   4560 Services                   0    11 148 Ko
wlanext.exe                   4692 Services                   0    10 876 Ko
conhost.exe                   4724 Services                   0     3 104 Ko
AsHidSrv64.exe                5052 Services                   0     2 036 Ko
ASUSOptimization.exe          5064 Services                   0     5 924 Ko
AsusSystemDiagnosis.exe       5088 Services                   0     3 004 Ko
AsusSystemAnalysis.exe        5096 Services                   0     7 488 Ko
svchost.exe                   5108 Services                   0    24 512 Ko
DTSAPO3Service.exe            5116 Services                   0     5 556 Ko
EvtEng.exe                    4208 Services                   0     9 956 Ko
AsusLiveUpdateAgent.exe       4216 Services                   0    14 084 Ko
esif_uf.exe                   4276 Services                   0     3 492 Ko
svchost.exe                   4272 Services                   0    43 224 Ko
svchost.exe                   4268 Services                   0     4 928 Ko
mfemms.exe                    4604 Services                   0     6 824 Ko
IntelCpHDCPSvc.exe            4680 Services                   0     3 836 Ko
svchost.exe                   4720 Services                   0    11 396 Ko
RegSrvc.exe                   4684 Services                   0     6 204 Ko
NvTelemetryContainer.exe      4740 Services                   0     8 416 Ko
ModuleCoreService.exe         4760 Services                   0    45 640 Ko
PEFService.exe                4764 Services                   0     1 024 Ko
svchost.exe                   4836 Services                   0     2 964 Ko
svchost.exe                   4852 Services                   0    19 800 Ko
OfficeClickToRun.exe          4908 Services                   0    41 640 Ko
RtkAudUService64.exe          5132 Services                   0     5 464 Ko
RstMwService.exe              5140 Services                   0     3 808 Ko
svchost.exe                   5164 Services                   0     7 904 Ko
ASUSDisplayCtrlService.ex     5172 Services                   0     8 508 Ko
GiftBoxService.exe            5180 Services                   0     6 384 Ko
sqlwriter.exe                 5188 Services                   0     4 404 Ko
mysqld.exe                    5220 Services                   0     4 876 Ko
svchost.exe                   5348 Services                   0    15 596 Ko
ZeroConfigService.exe         5368 Services                   0    13 968 Ko
vmnetdhcp.exe                 5376 Services                   0     3 816 Ko
vmnat.exe                     5408 Services                   0     5 384 Ko
svchost.exe                   5428 Services                   0     3 100 Ko
TeamViewer_Service.exe        5488 Services                   0    13 716 Ko
MsMpEng.exe                   5508 Services                   0   230 856 Ko
svchost.exe                   5560 Services                   0     2 632 Ko
svchost.exe                   5640 Services                   0    10 776 Ko
vmware-authd.exe              5648 Services                   0     9 472 Ko
vmware-usbarbitrator64.ex     5656 Services                   0     7 460 Ko
sqlservr.exe                  5796 Services                   0   134 340 Ko
sqlservr.exe                  5808 Services                   0   137 412 Ko
sqlceip.exe                   5816 Services                   0    35 036 Ko
ReportingServicesService.     5824 Services                   0   121 340 Ko
sqlceip.exe                   5836 Services                   0    34 132 Ko
ReportingServicesService.     5844 Services                   0   123 160 Ko
svchost.exe                   6100 Services                   0     5 744 Ko
svchost.exe                   6068 Services                   0     7 704 Ko
MMSSHOST.exe                  6548 Services                   0    34 116 Ko
IntelCpHeciSvc.exe            6632 Services                   0     3 532 Ko
mfevtps.exe                   6736 Services                   0     8 228 Ko
ProtectedModuleHost.exe       7136 Services                   0    11 384 Ko
svchost.exe                   8020 Services                   0     4 928 Ko
Microsoft.ReportingServic     3492 Services                   0    38 804 Ko
Microsoft.ReportingServic     2296 Services                   0    38 428 Ko
conhost.exe                   5292 Services                   0     4 368 Ko
conhost.exe                   8212 Services                   0     4 336 Ko
unsecapp.exe                  8708 Services                   0     7 216 Ko
WmiPrvSE.exe                  8848 Services                   0    10 260 Ko
mysqld.exe                    9540 Services                   0    17 108 Ko
NisSrv.exe                    9588 Services                   0     8 928 Ko
mfefire.exe                   9596 Services                   0     5 976 Ko
svchost.exe                  10312 Services                   0     7 180 Ko
fdlauncher.exe               10408 Services                   0     2 588 Ko
fdlauncher.exe               10420 Services                   0     2 564 Ko
Launchpad.exe                10520 Services                   0    10 984 Ko
Launchpad.exe                10528 Services                   0    10 936 Ko
svchost.exe                  10552 Services                   0    16 332 Ko
fdhost.exe                   10620 Services                   0     3 436 Ko
fdhost.exe                   10636 Services                   0     3 480 Ko
```

choisissez 5 services système et expliquer leur utilité
wininit.exe : c'est le programme de lancement de l'OS.

System Idle Process : c'est le programme qui tourne quand l'ordinateur n'a rien de mieux a faire.

System : c'est un programme qui se lance quand vous allumez votre PC.

smss.exe : c'est le programme de gestionnaire de session du sous-système, il gère toutes les app au démarrages.

csrss.exe : c'est un programme qui sert à gérer les fenêtres et les éléments graphiques de Windows.

Scripting :

Lien du script 1 :

Lien du script 2 : https://git.ynov-bordeaux.com/171646/projet-windows/blob/master/Desktop/projet_windows/script2.bat

### Gestion de softs

- Expliquer l'intérêt de l'utilisation d'un gestionnaire de paquets

L'intérêt d'utiliser un gestionnaire de paquets pour télécharger des paquets sur internet est la sécurité ajouté par le téléchargement en direct. De plus cela nous permet d'être sûr que les paquets soient bien installés sans pour autant qu'ils aient des virus. Les gestionnaires de paquets ont aussi des mesures de sécurité pour le téléchargement et peuvent les mettre à jour très rapidement.
Dans ce cas, sur Windows 10 on utilise la commande `choco`

- Utiliser un gestionnaire de paquet propres à votre OS pour :

  - lister tous les paquets déjà installés

```
PS C:\Users\Mathieu> choco list -li
Chocolatey v0.10.15
chocolatey 0.10.15
1 packages installed.

7-Zip 19.02 alpha|19.02 alpha
Active Directory Authentication Library pour SQL Server|14.0.800.90
Adobe Creative Cloud|5.1.0.407
Asus Dispslay Control Service|1.0.0
ASUS GiftBox Service|3.2.3.0
ASUS Hello|1.1.4.0
Asus Power Scheme|1.0.0
ASUS_FRQ_Control|1.0.8
Atom|1.43.0
Badlion Client 2.12.0|2.12.0
Blitz|1.6.46
BlueStacks App Player|4.140.11.1002
Browser pour SQL Server 2016|13.1.4001.0
Business Tour - Online Multiplayer Board Game|
Dashboard|1.0.0.6
Discord|0.0.306
DSB Notification|1.2.0
Enregistreur VSS Microsoft pour SQL Server 2016|13.1.4001.0
Epic Games Launcher|1.1.229.0
Fichiers de support d'installation de Microsoft SQL Server 2008|10.3.5500.0
FileZilla Client 3.48.0|3.48.0
Git version 2.23.0.windows.1|2.23.0.windows.1
GNS3|2.2.5
Google Chrome|81.0.4044.138
Google Cloud SDK|
Installation de Microsoft SQL Server 2016 (Français)|13.1.4001.0
Intel(R) Dynamic Platform and Thermal Framework|8.4.11000.6436
Intel(R) Management Engine Components|1823.12.0.1137
Intel(R) Rapid Storage Technology|16.5.0.1027
Intel(R) Serial IO|30.100.1727.1
Intel® OptaneT Pinning Explorer Extensions|16.8.0.1000
Intel® PROSet/Wireless Software|20.70.0.0u
Java 8 Update 231|8.0.2310.11
JetBrains PyCharm 2019.2.4|192.7142.42
League of Legends|
McAfee LiveSafe |16.0 R21
McAfee WebAdvisor|4.1.1.92
Microsoft .NET Framework 4.5 Multi-Targeting Pack|4.5.50710
Microsoft .NET Framework 4.5.1 Multi-Targeting Pack|4.5.50932
Microsoft .NET Framework 4.5.1 Multi-Targeting Pack (Français)|4.5.50932
Microsoft .NET Framework 4.5.1 SDK|4.5.51641
Microsoft .NET Framework 4.5.1 SDK (Français)|4.5.51641
Microsoft .NET Framework 4.5.2 Multi-Targeting Pack|4.5.51209
Microsoft .NET Framework 4.5.2 Multi-Targeting Pack (Français)|4.5.51209
Microsoft Help Viewer 1.1|1.1.40219
Microsoft Help Viewer 1.1 Language Pack - FRA|1.1.40219
Microsoft Help Viewer 2.2|2.2.23107
Microsoft MPI (7.0.12437.8)|7.0.12437.8
Microsoft ODBC Driver 13 for SQL Server|14.0.800.90
Microsoft Office 365 ProPlus - fr-fr|16.0.12527.20442
Microsoft OneDrive|19.232.1124.0012
Microsoft SQL Server 2012 Native Client |11.3.6518.0
Microsoft SQL Server 2016 T-SQL Language Service |13.0.14500.10
Microsoft SQL Server 2017 RC1|
Microsoft SQL Server Data-Tier Application Framework (x86) - fr-FR|14.0.3757.2
Microsoft SQL Server Management Studio - 17.2|14.0.17177.0
Microsoft SQL Server 2014 Management Objects |12.0.2000.8
Microsoft SQL Server 2016 (64 bits)|
Microsoft SQL Server 2016 T-SQL ScriptDom|13.1.4001.0
Microsoft System CLR Types pour SQL Server 2017 RC1|14.0.800.90
Microsoft System CLR Types pour SQL Server 2014|12.0.2402.11
Microsoft Teams|1.3.00.12058
Microsoft Visual C++ 2008 Redistributable - x86 9.0.30729.6161|9.0.30729.6161
Microsoft Visual C++ 2010  x64 Redistributable - 10.0.40219|10.0.40219
Microsoft Visual C++ 2010  x86 Redistributable - 10.0.40219|10.0.40219
Microsoft Visual C++ 2012 Redistributable (x64) - 11.0.61030|11.0.61030.0
Microsoft Visual C++ 2012 Redistributable (x86) - 11.0.61030|11.0.61030.0
Microsoft Visual C++ 2013 Redistributable (x64) - 12.0.21005|12.0.21005.1
Microsoft Visual C++ 2013 Redistributable (x64) - 12.0.21005|12.0.21005.1
Microsoft Visual C++ 2013 Redistributable (x64) - 12.0.40660|12.0.40660.0
Microsoft Visual C++ 2013 Redistributable (x86) - 12.0.21005|12.0.21005.1
Microsoft Visual C++ 2013 Redistributable (x86) - 12.0.21005|12.0.21005.1
Microsoft Visual C++ 2013 Redistributable (x86) - 12.0.40660|12.0.40660.0
Microsoft Visual C++ 2015-2019 Redistributable (x64) - 14.24.28127|14.24.28127.4
Microsoft Visual C++ 2015-2019 Redistributable (x86) - 14.23.27820|14.23.27820.0
Microsoft Visual Studio Code (User)|1.45.0
Minecraft Launcher|1.0.0.0
Module linguistique Microsoft Help Viewer 2.2 - FRA|2.2.23107
Mozilla Firefox 70.0.1 (x64 fr)|70.0.1
Mozilla Maintenance Service|70.0.1
MySQL Connector C++ 8.0|8.0.18
MySQL Connector J|8.0.18
MySQL Connector Net 8.0.18|8.0.18
MySQL Connector/ODBC 8.0|8.0.18
MySQL Documents 8.0|8.0.18
MySQL Examples and Samples 8.0|8.0.18
MySQL Installer - Community|1.4.31.0
MySQL Notifier 1.1.8|1.1.8
MySQL Router 8.0|8.0.18
MySQL Server 8.0|8.0.18
MySQL Shell 8.0.18|8.0.18
MySQL Workbench 8.0 CE|8.0.18
Nmap 7.80|7.80
Node.js|12.13.0
Npcap 0.9982|0.9982
NVIDIA 3D Vision Driver 398.35|398.35
NVIDIA GeForce Experience 3.14.0.139|3.14.0.139
NVIDIA HD Audio Driver 1.3.37.4|1.3.37.4
NVIDIA PhysX System Software 9.18.0628|9.18.0628
NVIDIA Pilote graphique 399.24|399.24
Oracle VM VirtualBox 6.0.14|6.0.14
Postman-win64-7.12.0|7.12.0
Prise en charge linguistique de Microsoft Visual Studio Tools for Applications 2015|14.0.23107.20
Python 3.7.4 (32-bit)|3.7.4150.0
Python 3.8.0 (32-bit)|3.8.150.0
Python Launcher|3.8.6860.0
RefreshRateService|1.0.16
Rocket League|
Service de langage T-SQL Microsoft SQL Server 2017 RC1|14.0.17177.0
Steam|2.10.91.91
Stratégies Microsoft SQL Server 2017 RC1|14.0.800.90
Teams Machine-Wide Installer|1.2.0.17057
TeamViewer|15.4.4445
Update for Windows 10 for x64-based Systems (KB4480730)|2.53.0.0
WinRAR 5.71 (32-bit)|5.71.0
Wireshark 3.0.6 64-bit|3.0.6
XAMPP|7.4.5-0
XMind ZEN 9.3.1|9.3.1
118 applications not managed with Chocolatey.
```

### Partage de fichiers

![](https://i.imgur.com/wpL59Gy.png)

### Chiffrement et notion de confiance

Expliquer en détail l'utilisation de certificats :

L'information principale d'un certificat est la clé publique, le certificat est donc infalsifiable : il est chiffré pour empêcher toute modification, et est nominatif, c'est-à-dire qu'il appartient à un seul site. De plus, il est délivré par une entité (comme la carte d’identité est délivrée à une personne et une seule) et certifié par les autorité car on voit apparaitre son "logo".

Cela permet donc aux certificats d'être sécurisé.

#### Chiffrement de mails

On génère des clés pour le client et le destinataire avec la commande `ssh-keygen -t rsa`ensuite a l'aide du logiciel SignTool.exe j'ai signé numériquement mes mails puis je l'ai envoyé a l'aide de gmail S/MIME.

### TLS

que garantit HTTPS par rapport à HTTP ?

Toutes les URL qui commencent par HTTP utilisent un protocole simple de transfert hypertexte, c’est grâce à ce protocole de réseaux standard que les navigateurs et les serveurs peuvent communiquer en échangeant des données.

HTTP est un système sans état, ce qui signifie qu’il permet de créer des connexions à la demande. Lorsque vous cliquez sur un lien, une connexion est sollicitée et votre navigateur web envoie la demande au serveur qui répond en ouvrant la page. Plus la connexion est rapide plus les données s’affichent rapidement.

L’unique objectif de HTTP est d’afficher les informations demandées sans se soucier de la façon dont ces informations se déplacent d’un endroit à un autre. Malheureusement, cela signifie que HTTP peut être intercepté et éventuellement détourné, ce qui rend les informations et leurs destinataires vulnérables.

HTTPS n’est pas l’opposé de HTTP mais plutôt son petit cousin. Tous deux sont des protocoles de transfert hypertexte qui permettent à des données web d’être affichées sur votre écran lorsque vous envoyez une requête. Cependant, HTTPS est légèrement différent, plus avancé et bien plus sécurisé.

En gros, le protocole HTTPS est une extension de HTTP. Le « S » à la fin est l’initiale du mot « Secure » (sécurisé) et il fonctionne grâce au protocole TLS (Transport Layer Security), le successeur du protocole SSL (Secure Sockets Layer), la technologie de sécurité standard pour établir une connexion chiffrée entre un serveur web et un navigateur.

Sans la présence de HTTPS, toutes les données que vous entrez sur un site (ex : nom d’utilisateur, mot de passe, carte bancaire, RIB ou tout autre information requise dans un formulaire) seront envoyées en format de texte brute et seront, par conséquent, vulnérables aux interceptions et à l’espionnage. C’est pour cette raison que vous devriez toujours vérifier qu’un site utilise bien HTTPS avant d’y entrer quelques données que ce soit.

En plus de chiffrer les données transmises entre un serveur et votre navigateur, le protocole TLS authentifie également le serveur auquel vous vous connectez et protège les données transmises de toute altération.

Pour vous aider à comprendre la différence, imaginez que HTTP dans HTTPS est l’équivalent d’une destination, tandis que SSL est l’équivalent d’un voyage. Le premier est chargé d’acheminer les données vers votre écran, le dernier gère la façon dont ces données sont déplacées. En joignant force, ils permettent aux flux de données d’être sécurisés.

## SSH

### Client

Deux clés sont générées par le client: une clé publique et une clé privée. Les deux sont liés, seul la clé publique peut déchiffrer un message chiffré par la clé privée et inversement. Elles sont crées avec la commande ssh-keygen.
On dépose donc la clé publique grâce à `ssh-copy-id dmathieu@10.4.2.2`. Sur dépose celle-ci car bien qu'ayant les mêmes propriétés, une seule clé doit être dévoilée pour maintenir la sécurité. Une clé est donc dite publique et c'est la seule qu'on partage.
Comme dis précédemment, seul notre clé publique peut déchiffrer un message chiffré par notre clé privée. Le serveur ayant notre clé publique, si on envoie un message chiffré, et que le serveur peut le déchiffré, alors qu'il est sûr que le message provient de nous.
La clé privée est stockée dans le dossier ~ / .ssh avec une autorisation de lecture et d'écriture seulement pour le super-utilisateur.

### L'empreinte digitale

Le fingerprint est l'empreinte SSH du serveur auquel on se connecte. Lors de notre connexion, soit notre PC a déjà vu cette IP et regarde si l'empreinte stockée dans known_host est la même; soit il n'a jamais vu cette IP et rajoute l'empreinte à l'hôte connu, d'où le oui | non. Cette sécurité permet d'être sûr que l'on se connecte bien à la bonne machine, et pas une machine ayant la même IP que celle qu'on veut joindre.

### ~ / .ssh / config

```
dmathieu@localhost:~/.ssh$ cat config
Host vm
    HostName 10.4.2.2
    User toto
    IdentityFile ~/.ssh/id_rsa.pub
```

### ssh jumping

```
Host jump
    User <jump-user>
    HostName <jump-host>
Host protected
    User <protected-user>
    HostName <protected-host>
    ProxyJump jump
```

Expédition de ports à domicile

### Configuration de la VM

Lorqu'une VM à une IP en bridge, elle est sûre le même réseau que l'hôte, elle peut donc accéder à toutes les machines du réseau local. Chez-moi, l'hôte à l'IP 192.168.1.26/24, et la VM 192.168.1.65/24

```
[mathieu@pc-554 ~]\$ ping -c 2 192.168.1.26
PING 192.168.1.26 ( 192.168.1.26) 56(84) bytes of data.
64 bytes from 192.168.1.26: icmp_seq=1 ttl=64 time=0.358 ms
64 bytes from 192.168.1.26: icmp_seq=2 ttl=64 time=0.516 ms

--- 192.168.1.26 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.358/0.437/0.516/0.079 ms
```
