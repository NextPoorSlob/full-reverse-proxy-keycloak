# Full Reverse Proxy Setup For Keycloak
This project sets up three Keycloak servers behind a NGINX service as a load balancer.

## Add Mappings To Hosts File
Add the following mappings to the _hosts_ file.  In Windows, it can be found in the
_C:\Windows\System32\drivers\etc_ directory. 
```text
127.0.0.1	keycloak admin.keycloak postgres
::1             keycloak admin.keycloak postgres
```

## Prepare a Self-Signed Certificate
Create a self-signed certificate in a keystore to test the set-up.
```shell
openssl genrsa -out keycloak.key 2048

openssl req -x509 -new -nodes -key keycloak.key \
    -sha256 -days 1024 -out keycloak.pem

 openssl pkcs12 -export \
    -name keycloak \
    -in keycloak.pem \
    -inkey keycloak.key \
    -out keycloak.keystore.p12
```

You can list the resulting  keystore with this line:
```shell
keytool -list -keystore keycloak.keystore.p12 -storepass keycloak
```

This sets up the keystore and certificates for Keycloak.
```shell
-- https-certificate-file=keycloak.crt

-- https-certificate-key-file=keycloak.pem

-- https-trust-store-file=keycloak.keystore.p12
```


