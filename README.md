# Yet Another Zcash Builder for Apple Platform

![Screenshot](https://github.com/kozyilmaz/zcash-apple/raw/master/docs/zcash-apple.png "Zcash on Mac OS")

This repository builds standalone Zcash binaries for macOS platform without installing brew.  
No additional dependency required, all tools (`autotools, cmake, gcc etc.`) and libraries (`boost`, `libsnark`) are compiled from scratch.  


### Build instructions

`$ git clone https://github.com/kozyilmaz/zcash-apple.git`  
`$ cd zcash-apple`  
`$ source environment`  
`$ make`

After successful build Zcash binaries will be installed to `out` directory under project root  
You can then copy binary directory anywhere you like there are no dependencies to the build tree anymore  
```
bash-3.2$ ls -lrt out/usr/local/bin/
total 104760
-rwxr-xr-x  1 loki  staff       483 Apr  4 18:47 zcash-init
-rwxr-xr-x  1 loki  staff  41668528 Apr  4 19:02 zcashd
-rwxr-xr-x  1 loki  staff   5797980 Apr  4 19:02 zcash-tx
-rwxr-xr-x  1 loki  staff      3502 Apr  4 19:02 zcash-fetch-params
-rwxr-xr-x  1 loki  staff   3006696 Apr  4 19:02 zcash-cli
-rwxr-xr-x  1 loki  staff   2644540 Apr  4 19:02 libstdc++.6.dylib
-rwxr-xr-x  1 loki  staff    245464 Apr  4 19:02 libgomp.1.dylib
-rw-r--r--  1 loki  staff    255268 Apr  4 19:02 libgcc_s.1.dylib
bash-3.2$ otool -L out/usr/local/bin/zcashd
out/usr/local/bin/zcashd:
    @executable_path/libstdc++.6.dylib (compatibility version 7.0.0, current version 7.22.0)
    @executable_path/libgomp.1.dylib (compatibility version 2.0.0, current version 2.0.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.51.1)
    @executable_path/libgcc_s.1.dylib (compatibility version 1.0.0, current version 1.0.0)
```

### Run instructions

When launching `Zcash` on MacOS for the first time, certain initalization steps should be completed.  
Please run the commands below once for the first time  

`$ cd out/usr/local/bin`  
`$ ./zcash-fetch-params`  
`$ ./zcash-init`  
`$ ./zcashd`  

You can just run `Zcash` by launching the daemon afterwards  

`$ ./zcashd`  

Vaklinov's [Desktop GUI Wallet](https://github.com/vaklinov/zcash-swing-wallet-ui) also works, please follow [build instructions for MacOS](https://github.com/vaklinov/zcash-swing-wallet-ui/blob/master/docs/Readme-Mac.md)

Console output from the first run is below:
```
bash-3.2$ ./zcash-fetch-params
Zcash - fetch-params.sh

This script will fetch the Zcash zkSNARK parameters and verify their
integrity with sha256sum.

If they already exist locally, it will exit now and do nothing else.
The parameters are currently just under 911MB in size, so plan accordingly
for your bandwidth constraints. If the files are already present and
have the correct sha256sum, no networking is used.

Creating params directory. For details about this directory, see:
/Users/loki/Library/Application Support/ZcashParams/README

Retrieving: https://z.cash/downloads/sprout-proving.key
######################################################################## 100.0%
/Users/loki/Library/Application Support/ZcashParams/sprout-proving.key.dl: OK
/Users/loki/Library/Application Support/ZcashParams/sprout-proving.key.dl -> /Users/loki/Library/Application Support/ZcashParams/sprout-proving.key
Retrieving: https://z.cash/downloads/sprout-verifying.key
######################################################################## 100.0%
/Users/loki/Library/Application Support/ZcashParams/sprout-verifying.key.dl: OK
/Users/loki/Library/Application Support/ZcashParams/sprout-verifying.key.dl -> /Users/loki/Library/Application Support/ZcashParams/sprout-verifying.key
bash-3.2$ 
bash-3.2$ cat zcash-init 
#!/bin/bash

# excerpted from zclassic/zutil/init-mac.sh

if [ ! -f "$HOME/Library/Application Support/Zcash/zcash.conf" ]; then
    echo "Creating zcash.conf"
    mkdir -p "$HOME/Library/Application Support/Zcash/"
    echo "rpcuser=zcashrpc" > ~/Library/Application\ Support/Zcash/zcash.conf
    PASSWORD=$(cat /dev/urandom | env LC_CTYPE=C tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)
    echo "rpcpassword=$PASSWORD" >> "$HOME/Library/Application Support/Zcash/zcash.conf"
    echo "Complete!"
fi
bash-3.2$ 
bash-3.2$ ./zcash-init 
Creating zcash.conf
Complete!
```

## Thanks
Developers of `Zcash`  
Developers of `ZClassic` for MacOS patches

## Donations
If you feel this project is useful to you. Feel free to donate.

    BTC address: 1GmXRm5sEATy3Kz1hCxS1dwfXuCPkevsa
    ZEC address: t1MW8Vx4SF1ewmL3rTN8UfRxULFTaugh1ab


### Disclaimer
This program is not officially endorsed by or associated with the Zcash project and the Zcash company.
[Zcash®](https://trademarks.justia.com/871/93/zcash-87193130.html) and the 
[Zcash® logo](https://trademarks.justia.com/868/84/z-86884549.html) are trademarks of the
[Zerocoin Electric Coin Company](https://trademarks.justia.com/owners/zerocoin-electric-coin-company-3232749/).

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

