# HyperVBackup

HyperVBackup is, as you can guess, a utility that can perform backups of HyperV virtual machines. It uses Volume Shadow Services (VSS) so it can back up running virtual machines. 

It started as a fork of http://hypervbackup.codeplex.com, as it was evident that the original creators weren’t going to update it anymore. So we added some features that we and the community were needing.

Beware that this project is a heavily modified version of the original source code with a lot of features added (7zip format support, individual files filter, updated to .Net Framework 4.6, etc.). If you want a closer version to the original code visit http://hypervbackup.codeplex.com/discussions/567463. 

You can see all options executing the program without arguments, currently those are:

```
f, file              Text file containing a list of VMs to backup, one per line.
l, list              List of VMs to backup, comma separated.
v, vhdinclude        List of VHDs file names to backup, comma separated.
i, vhdignore         List of VHDs file names to ignore, comma separated.
a, all               (Default: True) Is set, backup all VMs on this server.
n, name              (Default: True) If set, VMs to backup are specified by name.
g, guid              If set, VMs to backup are specified by guid.
o, output            Required. Backup ouput folder.
p, password          Secure the backup with a password.
z, zip               Use the zip format to store the backup.
d, directcopy        Do not compress the output, just copy the files recreating the folder structure.
outputformat         Backup archive name format. {0} is the VM's name, {1} the VM's GUID, {2} is the current date and time and {3} is the extension for the compression format (7z or zip).
                     Default: "{0}_{2:yyyyMMddHHmmss}{3}"
s, singlevss         Perform one single snapshot for all the VMs.
compressionlevel     (Default: 3) Compression level, between 0 (no compression, very fast) and 9 (max. compression, very slow).
cleanoutputbydays    (Default: 0) Delete all files in the output folder older than x days. TOTALLY OPTIONAL. USE WITH CAUTION.
cleanoutputbymb      (Default: 0) Delete older files in the output folder if total size is bigger then x Megabytes. TOTALLY OPTIONAL. USE WITH CAUTION.
```

For example, if you want to backup the Mail Server virtual machine on \\\shared\backups folder you use:

```HyperVBackup -l "Mail Server" -o "\\shared\backups" --compressionlevel 0```

Note: short switchs use one dash (-) / long switches use two dashes (--).

HyperVBackup only works on HyperV Server (Windows Server 2012, 2012 R2 and 2016 supported) and DOESN’T work on HyperV Client (Windows 8, 8.1 or 10).

The output is stored in 7zip format (you must provide the 7z.dll file corresponding to the version you want to use, included is version 15.14). You can use the zip format for the output, but the 7Zip libraries are still required, as they are used as the compression engine.


More information [in the Wiki] (https://github.com/ColiseoSoftware/hypervbackup/wiki)

**Troubleshooting**

* If you find the following error when you run the program: System.MissingMethodException: Method not found System.Array.Empty() you are probably running the Net Framework 4.5, you need to install version 4.6.

* If you find the following error when you run the program: Could not load file or assembly AlphaVSS.60x64.dll you need to install the Microsoft Visual C++ 2010 SP1 Redistributable Package.


**Related projects**


If you want to further automate the backup process try
https://github.com/nelsh/HVbackupLaunch


