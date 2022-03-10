
# gateway

85.230.176.77

# tun or tap

* [tun tap diff](https://proprivacy.com/guides/tun-tap)

tun at layer 3   - could encrypt
tap at layer 2  - could forward non-ip packet

* [maybe interesting](https://serverfault.com/questions/21157/should-i-use-tap-or-tun-for-openvpn)

# windows

when use openvpn gui and the .ovpn config file this is the adapter 

```bash
Unknown adapter OpenVPN TAP-Windows6:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::6ded:4a40:aad2:4cf4%71
   IPv4 Address. . . . . . . . . . . : 10.8.0.10
   Subnet Mask . . . . . . . . . . . : 255.255.255.252
   Default Gateway . . . . . . . . . :
```

## easyrsa

* [video setup](https://www.youtube.com/watch?v=s9SMg8GrnLw)

* [openssl, openvpn easyrsa francais](https://www.youtube.com/watch?v=Fz1m3RR313w)


* install [scoop](https://scoop.sh/)
need to install .NET, also [here video](https://www.youtube.com/watch?v=dwPFWzncyoo)

* [install gsudo](https://stackoverflow.com/questions/9652720/how-to-run-sudo-command-in-windows#:~:text=There%20is%20no%20sudo%20command,choosing%20%22run%20as%20administrator.%22&text=runas%20is%20elevation%20of%20a,Administrators%3B%20sudo%20is%20another%20thing.)

`scoop gsudo`

## server vpn 

* [tutorial](https://supporthost.in/how-to-install-and-configure-openvpn-on-windows-10/)

```bash
-----
Common Name (eg: your user, host, or server name) [Easy-RSA CA]:ServerVPN

CA creation complete and you may now import and sign cert requests.
Your new CA certificate file for publishing is at:
C:/Program Files/OpenVPN/easy-rsa/pki/ca.crt


```

* build rsa key

```powershell
# ./easyrsa build-server-full ServerVPN nopass

Note: using Easy-RSA configuration from: ./vars
Using SSL: openssl OpenSSL 1.1.1i  8 Dec 2020
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp4363.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp4363.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp449C.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp449C.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp4642.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp4642.tmp
fd = 3
Generating a RSA private key
..............+++++
.................................................................................................+++++
writing new private key to 'C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.a26528'
-----
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp4F6A.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp4F6A.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp540D.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp540D.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp5749.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp5749.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp5882.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp5882.tmp
fd = 3
Using configuration from C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-25328.a35800/tmp.a34340
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'ServerVPN'
Certificate is to be certified until Jun 11 14:22:07 2024 GMT (825 days)

Write out database with 1 new entries
Data Base Updated
```

* check the certificate

```powershell
EasyRSA Shell
# openssl verify -CAfile pki/ca.crt pki/issued/ServerVPN.crt
pki/issued/ServerVPN.crt: OK
```

* create client pki

```powershell
EasyRSA Shell
# ./easyrsa build-client-full ClientVPN nopass

Note: using Easy-RSA configuration from: ./vars
Using SSL: openssl OpenSSL 1.1.1i  8 Dec 2020
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-4948.a23180/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp3FEA.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp3FEA.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-4948.a23180/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp40F4.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp40F4.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-4948.a23180/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp421D.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp421D.tmp
fd = 3
Generating a RSA private key
.................................................................................+++++
..........+++++
writing new private key to 'C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-4948.a23180/tmp.a32208'
-----
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-4948.a23180/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp4B54.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp4B54.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-4948.a23180/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp4DD5.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp4DD5.tmp
fd = 3
path = C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-4948.a23180/tmp.XXXXXX
lpPathBuffer = C:\Users\hupan\AppData\Local\Temp\
szTempName = C:\Users\hupan\AppData\Local\Temp\tmp4EEE.tmp
path = C:\Users\hupan\AppData\Local\Temp\tmp4EEE.tmp
fd = 3
Using configuration from C:/Program Files/OpenVPN/easy-rsa/pki/easy-rsa-4948.a23180/tmp.a04868
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'ClientVPN'
Certificate is to be certified until Jun 11 14:25:21 2024 GMT (825 days)

Write out database with 1 new entries
Data Base Updated
```

* verify client PKI

```powershell
EasyRSA Shell
# openssl verify -CAfile pki/ca.crt pki/issued/ClientVPN.crt
pki/issued/ClientVPN.crt: OK
```

* tls create

```powershell
EasyRSA Shell
# ./easytls init-tls

Saved CA Identity: ./pki/easytls/data/easytls-ca-identity.txt

init-tls complete; you may now create TLS keys and .inline files.
  Your newly created TLS dir is:

    ./pki/easytls

To configure your Easy-TLS custom group now, use:
    'easytls config custom.group YOUR_GROUP'

To configure your Easy-TLS temporary directory now, use:
    'easytls config tmp.dir YOUR_DIR'

Recommended temporary directory setting:
    Windows - C:/Windows/Temp (Use '/' NOT '\')

```

* generate `tls-auth` key

```powershell
EasyRSA Shell
# ./easytls build-tls-auth

TLS auth key created: ./pki/easytls/tls-auth.key
```

* generate deffie-hellman parameters

```powershell
EasyRSA Shell
# ./easyrsa gen-dh

Note: using Easy-RSA configuration from: ./vars
Using SSL: openssl OpenSSL 1.1.1i  8 Dec 2020
Generating DH parameters, 2048 bit long safe prime, generator 2
This is going to take a long time
.......................................................+...............................................+.........................................................................+..............................................................................................................+........................................................................+...........................................................................................................................................................................+.........................................................................................................................+......................................................................................................................................++*++*++*++*

DH parameters of size 2048 created at C:/Program Files/OpenVPN/easy-rsa/pki/dh.pem

```

* firewall rule

```powershell
PS C:\Users\hupan> New-NetFirewallRule -DisplayName "OpenVPN" -Direction inbound -Profile Any -Action Allow -LocalPort 1194 -Protocol UDP


Name                          : {de4de7cf-7558-4ea9-a188-f0412c8bc785}
DisplayName                   : OpenVPN
Description                   :
DisplayGroup                  :
Group                         :
Enabled                       : True
Profile                       : Any
Platform                      : {}
Direction                     : Inbound
Action                        : Allow
EdgeTraversalPolicy           : Block
LooseSourceMapping            : False
LocalOnlyMapping              : False
Owner                         :
PrimaryStatus                 : OK
Status                        : The rule was parsed successfully from the store. (65536)
EnforcementStatus             : NotApplicable
PolicyStoreSource             : PersistentStore
PolicyStoreSourceType         : Local
RemoteDynamicKeywordAddresses : {}
```

* default assigned ip of the openvpn server

```powershell
Unknown adapter OpenVPN TAP-Windows6:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::1175:e364:896:3714%77
   IPv4 Address. . . . . . . . . . . : 10.8.0.1
   Subnet Mask . . . . . . . . . . . : 255.255.255.252
   Default Gateway . . . . . . . . . :

```

## client side

* tls-auth

```config
tls-auth "C:\\Program Files\\OpenVPN\\easy-rsa\\pki\\easytls\\tls-auth.key" 1 # This file is secret

```

Note it is changed to  1 instead of `0` for the server

# linux

start

`openvpn --config client.ovpn` 

to stop [here](https://unix.stackexchange.com/questions/424719/how-do-i-stop-daemonized-openvpn-connection)

```bash
sudo openvpn3 session-manage --disconnect --config $'client'.ovpn
```

* [good tutorial](https://www.cyberciti.biz/faq/howto-setup-openvpn-server-on-ubuntu-linux-14-04-or-16-04-lts/)

Seems the `sudo bash openvpn-install.sh` can do many things (create new client, revoke ca e.g.)


* generate server

Name is `ServerTest`

```bash
 ./easyrsa build-server-full S
erverTest nopass

Note: using Easy-RSA configuration from: /etc/openvpn/server/easy-rsa/vars
Using SSL: openssl OpenSSL 1.1.1  11 Sep 2018
Generating a RSA private key
.......................................................................................+++++
.................................................................................+++++
writing new private key to '/etc/openvpn/server/easy-rsa/pki/easy-rsa-4888.XTvooV/tmp.yA5Sin'
-----
Using configuration from /etc/openvpn/server/easy-rsa/pki/easy-rsa-4888.XTvooV/tmp.IjWZ0c
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'ServerTest'
Certificate is to be certified until Jun 12 09:47:09 2024 GMT (825 days)

Write out database with 1 new entries
Data Base Updated

```

* create client side pki, name

`ClientTest`

```bash
 ./easyrsa build-client-full C
lientTest nopass

Note: using Easy-RSA configuration from: /etc/openvpn/server/easy-rsa/vars
Using SSL: openssl OpenSSL 1.1.1  11 Sep 2018
Generating a RSA private key
.................................................................................................................................+++++
.........+++++
writing new private key to '/etc/openvpn/server/easy-rsa/pki/easy-rsa-5011.BwJIAb/tmp.tiL1AD'
-----
Using configuration from /etc/openvpn/server/easy-rsa/pki/easy-rsa-5011.BwJIAb/tmp.zyWF58
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'ClientTest'
Certificate is to be certified until Jun 12 09:50:10 2024 GMT (825 days)

Write out database with 1 new entries
Data Base Updated
```


## procedure

More information can be found at [online wiki](https://community.openvpn.net/openvpn/wiki/EasyRSA3-OpenVPN-Howto)

1. go to `/etc/openvpn/easy-rsa/`  type `./easyrsa init-pki`
2. create CA: `./easyrsa build-ca nopass`
3. build server certifcate `./easyrsa build-server-full ServerTest nopass`

> Option nopass can be used to disable password locking the key.

4. verify the server certificate

```bash
openssl verify -CAfile pki/ca.crt pki/issued/ServerTest.crt
```

5.  create client certificate `./easyrsa build-server-full ServerTest nopass`
6. verify the client certificate

```bash
openssl verify -CAfile pki/ca.crt pki/issued/ClientTest.crt
```

7. go to [tls]( https://github.com/TinCanTech/easy-tls) and clone the fine `easytls` to the folder `easyrsa` type

```bash
./easytls init-tls
```

create `TLS_AUTH` key

```bash
./easytls build-tls-auth
```

8. generating DH parameter

```bash
./easytls build-tls-auth
```

9. change the `server.conf`

```conf
ca /etc/openvpn/server/easy-rsa/pki/ca.crt
cert /etc/openvpn/server/easy-rsa/pki/issued/ServerTest.crt
key /etc/openvpn/server/easy-rsa/pki/private/ServerTest.key  # This file should be kept secret

# Diffie hellman parameters.
# Generate your own with:
#   openssl dhparam -out dh2048.pem 2048
dh /etc/openvpn/server/easy-rsa/pki/dh.pem
...
tls-auth /etc/openvpn/server/easy-rsa/pki/easytls/tls-auth.key 0 # This file is secret

```


10. For the client side, 

```conf
ca "C:\\Program Files\\OpenVPN\\config\\ca.crt"

cert "C:\\Program Files\\OpenVPN\\config\\ClientTest.crt"

key "C:\\Program Files\\OpenVPN\\config\\ClientTest.key"  # This file should be kept secret

tls-auth "C:\\Program Files\\OpenVPN\\config\\tls-auth.key" 1 # This file is secret


```

**Note** it seems the file has to be exactly in that `config` folder where your `openvpn` PATH variable has been set to.

## trouble-shooting

* [peer certificate verification failure](https://forums.openvpn.net/viewtopic.php?f=37&t=32568)

Basically check the `ca.crt` is correctly configured.

* [standing initialization](https://forums.openvpn.net/viewtopic.php?t=25036)

Basically means that server is now working and listnening on the port.