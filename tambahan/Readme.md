File Tambahan

<b>Untuk OS Raspbian Raspberry Pi-1,2,3</b>
<br>
1.	Copy file SSH ke Root SD setelah proses burning
<br>

<b>Untuk OS Raspbian Raspberry Pi Zero /W</b>
<br>

1.	Copy file SSH ke Root SD setelah proses burning
<br>

2.	Buka file config.txt dengan Notepad++/Sublim
	-	Tambahkan baris terakhir --> dtoverlay=dwc2
<br>

3.	Buka file config.txt 
		Tambahkan modules-load=dwc2,g_ether setelah rootwait
