```
    _              _           _     _   ____ ____  _     
   / \   _ __   __| |_ __ ___ (_) __| | / ___/ ___|| |    
  / _ \ | '_ \ / _` | '__/ _ \| |/ _` | \___ \___ \| |    
 / ___ \| | | | (_| | | | (_) | | (_| |  ___) |__) | |___ 
/_/   \_\_| |_|\__,_|_|  \___/|_|\__,_| |____/____/|_____|
                                                          
 ____  _             _             
|  _ \(_)_ __  _ __ (_)_ __   __ _ 
| |_) | | '_ \| '_ \| | '_ \ / _` |
|  __/| | | | | | | | | | | | (_| |
|_|   |_|_| |_|_| |_|_|_| |_|\__, |
                             |___/ 
```


Majority of android devices use ssl pinning, which basically means that every android application will carry its own set of ssl certificates, which basically
becomes the foundation for ssl verifications
This is usually a very secure thing, however when we really want to understand the apis, or if we ever want to perform those api calls on our own, it becomes challenging to reverse engineer them

Hence, this guide for the same.

### Evasion Methods

There are quite a few evasion methods, as follows
1. Use `apk-mitm` to bypass the ssl pinning by decompiling the app, and then removing the ssl pins.
2. Use the `LSPatch` or `NPatch` to install `justtrustmepro` to disable the ssl pin for the specific app
3. Use a rooted phone and add the CA certs into the phone system CA, that way you are always trusted
4. Use android-unpinner to patch the app to not have the ssl pinned, which is by far the best way to do this as per my work and tests
5. Unpack the application and inject custom CA into the pinned ssl certs

### How to Android un-Pinning

https://github.com/mitmproxy/android-unpinner
Tbh, its not the first time python script has saved me lots of troubles, and quoting:

> Does not require root.
> Uses frida-apk to mark app as debuggable. This is much less invasive than other approaches, only AndroidManifest.xml is touched within the APK.
> Includes a custom Java Debug Wire Protocol implementation to inject the Frida Gadget via ADB.
> Uses HTTPToolkit's excellent unpinning script to defeat certificate pinning.
> Already includes all native dependencies for Windows/Linux/macOS (adb, apksigner, zipalign, aapt2).
> Handles XAPKs by extracting the split APKs, unpinning them and installing them with adb install-multiple.

I have no complaints,

using this I first installed the app onto my system from google playstore, 

```
uv tool install git+https://github.com/mitmproxy/android-unpinner
```

1. Make a directory for working!
```
cd ~/tmp
mkdir -p reversingTruecaller
cd reversingTruecaller
```

1. Fetch the APK `android-unpinner get-apks com.truecaller .`
2. Patch the APK `android-unpinner patch-apks *.apk`
3. Install the patched APK `android-unpinner install *.unpinned.apk`, Perform the verification + Validation with the OTP
4. Install httptoolkit (or burp or mitmproxy or pcapdroid whichever suits to your taste)
5. Attach your android device via ADB, start the httptoolkit capture on phone (read their docs on how to)
6. Start capture, perform a search and check the results in the monitor screen, you should be able to find the correct request for the same


### Sample Code

This is viable to change in the future, but since the truecaller folks use protobuf (and I didnt feel the need to build the schema for effortless decoding I used `protoc`), Following code should work ootb

```
import requests
import subprocess

url = (
    'https://search5-noneu.truecaller.com/v2/search'
    # '?q=dummynumberyouwanttosearch'
    '?q=[7911111111111](7911111111111)'
    '&countryCode=IN'
    '&type=4'
    '&encoding=json'
)

headers = {
    'Accept': 'application/x-protobuf',
    'Accept-Encoding': 'gzip',
    'Authorization': 'Bearer a2i0F--DidYOuReallyThinkThisistheCorrectToken?-Sorrybutitsnotthisisfillertextpewpew',
    'Connection': 'Keep-Alive',
    'Host': 'search5-noneu.truecaller.com',
    'User-Agent': 'Truecaller/16.6.6 (Android;15)'
}

response = requests.get(url, headers=headers, timeout=10)

print('Status:', response.status_code)
print('Response headers:', response.headers)

# protobuf binary
data = response.content
print('Protobuf size:', len(data))

# ---- integrate protoc decode_raw ----
proc = subprocess.Popen(
    ['protoc', '--decode_raw'],
    stdin=subprocess.PIPE,
    stdout=subprocess.PIPE,
    stderr=subprocess.PIPE
)

stdout, stderr = proc.communicate(data)

if stderr:
    print('protoc error:', stderr.decode())

print('\n===== DECODED (schema-less) =====')
print(stdout.decode(errors='replace'))

```
