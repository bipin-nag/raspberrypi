# WiFi

Guides :

- https://openwrt.org/docs/guide-quick-start/basic_wifi
- https://openwrt.org/docs/guide-user/network/wifi/encryption

Steps:

1. uci show wireless
2. uci set wireless.radio0.country='IN'
3. uci set wireless.radio0.disabled='0'
4. uci set wireless.default_radio0.encryption='psk2'
5. uci set wireless.default_radio0.key='password'
6. uci commit wireless
7. wifi reload
