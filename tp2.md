# TP 2 Maîtrise de poste

## Sujet 2 Débugger et désassembler des programmes compilés

Dans un premier temps on fait l'installalation de "gdb" qui est un débugger et "ghidra" qui est un désassembleur sur ubuntu

Pour compiler le programme "Hello World", on tape la commande :

`gcc -g hw.c -o hw`

Ensuite on execute le programme Hello World compilé

dmathieu@dmathieu-VirtualBox:~/Documents/masteringhost\$ ./hw
Hello, World!

Une fois assemblé, on désassemble "main" avec la commande : `(gdb) disass main` ce qui donne :

```
(gdb) disass main
Dump of assembler code for function main:
   0x000000000000064a <+0>:	push   %rbp
   0x000000000000064b <+1>:	mov    %rsp,%rbp
   0x000000000000064e <+4>:	lea    0x9f(%rip),%rdi        # 0x6f4
   0x0000000000000655 <+11>:	mov    $0x0,%eax
   0x000000000000065a <+16>:	callq  0x520 <printf@plt>
   0x000000000000065f <+21>:	mov    $0x0,%eax
   0x0000000000000664 <+26>:	pop    %rbp
   0x0000000000000665 <+27>:	retq
End of assembler dump.
```

Je pense que le "Hello, World!" est stocké dans "callq". Elle est affiché en entier sans oublié une lettre de "Hello World" dans le terminal

Ayant eu des problème sous ubuntu, je suis repassé sur Windows pour le crack de Winrar et j'installe le package "resource hacker".

Une fois l'opération faite, sur "resource hacker" on effectue les manipulations suivantes: on ouvre Open WinRAR.exe > dialog > REMINDER clique droit puis delete > et le fichier save as fini.

## Sujet 4 Analyse de boot

Pour ces exercices je suis sur une vm CentOs 7

Mes 5 programmes les plus long à démarrer sont :

    - apt-daily-upgrade.service (~1m23s)
    - apt-daily.service (~44s)
    - sqlservr.exe (~30s)
    - vboxadd.service (~9s)
    - vmware-authd.exe (~8s)

On va ensuite analyser les logs de boot du noyau avec la commande `dmesg` : ce qui donne :

```
cpu, bios physical ram, ramdisk
linux version 5.3.0-59.63~18.04.1-generic
    les 5 lignes qui semblent pour moi très importantes :
mount-cache hash table entries : ram physique réservée
systemd : tout ce qui concerne le systeme
os product : qui à produit l'os
os release : l'identification du systeme ?
os version : la version de l'os
non le dernier log est "btrfs loaded"
```
