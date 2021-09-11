# WiFi

Guides :
- https://openwrt.org/docs/guide-quick-start/basic_wifi
- https://openwrt.org/docs/guide-user/network/wifi/encryption

Steps:

1. ssh root@192.168.1.1

2. uci show wireless

3. uci set wireless.radio0.country='IN'

4. uci set wireless.radio0.disabled='0'

5. uci set wireless.default_radio0.encryption='psk2'

6. uci set wireless.default_radio0.key='=v^K9s5duJTFkC5^'

7. uci commit wireless

8. wifi reload
