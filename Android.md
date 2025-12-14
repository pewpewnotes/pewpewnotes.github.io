### Android
* How to Evade SSL Pinning in Android (And Much more?) - [AndroidSSLPinning](AndroidSSLPinning)

#### Enable VPN Always for Android

1. Enabling always-on VPN for androidTV 

`adb shell settings put secure always_on_vpn_app com.tailscale.ipn`

```

adb shell settings put secure always_on_vpn_lockdown 0
adb shell settings put secure always_on_vpn_lockdown_whitelist
```


