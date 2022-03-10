

# openvpn

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