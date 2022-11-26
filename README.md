<h1>How to restore IMEI (even if you don't have a backup)</h1>
<b>Original instruction by slfl from 4pda.to</b>
<be>
Needed tools:
<a href="https://spflashtool.com/">SP Flash Tool</a>, MAUI META

1. Completely format the phone (format all), remove the garbage.
2. Unlock the bootloader and flash one of these files, depnding on your phone region:<br>
<a href="https://github.com/camellian-devs/IMEI-restore/blob/main/files/nvram_china.zip">nvram_china.zip</a><br>
<a href="https://github.com/camellian-devs/IMEI-restore/blob/main/files/nvram_global.zip">nvram_global.zip</a>
3. Flash the engineer ROM with Firmware upgrade, then repeat with Download (thus we remove the rescue / cust error)
4. After downloading the firmware, it is important to make sure in the CIT (phone test program) that we have the IMEI. It will not be displayed in the phone settings!
5. If everything is fine, reboot the phone into fastboot and clean the nvdata / nvram partitions:
fastboot erase nvdata
fastboot erase nvram
6. Launch Maui Meta. We will need to choose to download the database, but it does not load from the phone, so we take this archive:
Maui Meta

7. Maui Meta swears, but allows you to edit the data in the phone. We look for "Update Patameter" in the search and then load this file (in the archive):
IMEI

8. Be sure to edit the ini file! 510, 511, 990, 991 lines. Here you need to enter your ESN, MEID, IMEI. Then we write the file to the phone.
9. Then try to turn on the phone and you will get a bootloop - this is normal
10. Boot into fastboot and flash NVRAM: fastboot flash nvram your_nvram.img 
and then reboot
11. The engineer ROM should boot normally, your IMEI and version of the modem should have appeared in the settings.
12. Flash the stock ROM

13. Remove dm-verity error if needed. Either with vbmeta patch or format the seccfg section: Address 0x15000000, partition size 0x800000.


It is important to understand that even if you made a backup of nvdata and flashed it back, you may not have it. Why? Because Xiaomi made it this way and the device is specific
