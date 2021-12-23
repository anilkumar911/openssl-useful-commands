# openssl-useful-commands
Useful openssl commands

* Create server certificate signed by CA

Source: https://mariadb.com/docs/security/encryption/in-transit/create-self-signed-certificates-keys-openssl/

```
$ openssl genrsa 2048 > ca-key.pem

$ openssl req -new -x509 -nodes -days 365000 \
   -key ca-key.pem \
   -out ca-cert.pem

$ openssl req -newkey rsa:2048 -nodes -days 365000 \
   -keyout server-key.pem \
   -out server-req.pem

$ openssl x509 -req -days 365000 -set_serial 01 \
   -in server-req.pem \
   -out server-cert.pem \
   -CA ca-cert.pem \
   -CAkey ca-key.pem
```

* Single line command to generate self signed sertificate:
```
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 365 -nodes
```

* Single line command to generate certificate with key usage extensions
```
openssl req -x509 -nodes -newkey rsa:2048 -keyout key.pem -out server.pem -days 7300 -subj '/CN=My Name/C=US/OU=My Unit/O=ACME' -addext "keyUsage = digitalSignature, keyEncipherment, dataEncipherment, cRLSign, keyCertSign" -addext "extendedKeyUsage = serverAuth, clientAuth"
```
