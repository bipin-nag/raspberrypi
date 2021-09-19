# Adblock

Guides :

- https://openwrt.org/docs/guide-user/services/ad-blocking

Steps:

1. opkg update
2. opkg install adblock
3. opkg install luci-app-adblock
4. opkg install aria2 tcpdump-mini
5. uci set adblock.global.adb_backupdir="/etc/adblock"
6. uci commit adblock
7. /etc/init.d/adblock restart
