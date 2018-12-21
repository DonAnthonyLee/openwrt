## How to use the RTL8188EU driver on OpenWrt

Run the following commands to enable client mode by "wpad-mini".

	# wpa_supplicant -B -iwlan0 -Dwext -c/etc/wpa_supplicant.conf
	# udhcpc -i wlan0

