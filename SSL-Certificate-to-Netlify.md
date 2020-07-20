1. Export `docs.nml.co.za` certificate from Azure
1. Import into your user certificate store
1. Export with key (no extended attributes)
1. Extract certificate, key file, and chain with the following:

Key
```
openssl pkcs12 -in filename.pfx -nocerts -out cert_key.pem
```
Certificate
```
openssl pkcs12 -in filename.pfx -clcerts -nokeys -out cert.pem
```

Chain
```
openssl pkcs12 -in filename.pfx -cacerts -nokeys -out cert_chain.pem
```

# openssl rsa -in key.pem -out server.key 