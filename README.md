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
