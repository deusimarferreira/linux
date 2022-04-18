# Verificando Certificado e Chave
A maneira mais simples para verificar se uma chave privada é valida para um certificado é gerando o hash de ambos e depos comparar o resultado.

**Observação**: Os dados utilizados neste exemplo foram gerados apenas para testes e por esse motivo disponibilizamos a nossa chave privada, essa chave é pessoal/serviço e intransferivél, em hipótese alguma disponibilize sua chave privada para terceiros. 

> Vamos adicionar a chave privada em um arquivo
~~~sh
$ cat << EOF > minha-chave-privada.key
-----BEGIN PRIVATE KEY-----
MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQghyE7RYuiSmbJf4PT
y454Jas8/EXKU1rPmS9FCz9hoXuhRANCAAQX3DY0E6KiH8mHKy7TPyJkXLmGUyYt
FWSIeItWOLR4dZkRCAfWV5gOwZMTQ3G5+4vyzhWJBHWVK7d5fDAJLMZW
-----END PRIVATE KEY-----
EOF
~~~

> Vamos adicionar o certificado em um arquivo
~~~sh
$ cat << EOF > meu-certificado.pem
-----BEGIN CERTIFICATE-----
MIICVjCCAfygAwIBAgIRANkAJyUBb5fF4QYs8SD4IM8wCgYIKoZIzj0EAwIwdTEL
MAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNhbiBG
cmFuY2lzY28xGjAYBgNVBAoTEW9yZzEudmlsbGFsYWJzLmNvMR0wGwYDVQQDExRj
YS5vcmcxLnZpbGxhbGFicy5jbzAeFw0yMDA1MTMwMjMyMDBaFw0zMDA1MTEwMjMy
MDBaMHUxCzAJBgNVBAYTAlVTMRMwEQYDVQQIEwpDYWxpZm9ybmlhMRYwFAYDVQQH
Ew1TYW4gRnJhbmNpc2NvMRowGAYDVQQKExFvcmcxLnZpbGxhbGFicy5jbzEdMBsG
A1UEAxMUY2Eub3JnMS52aWxsYWxhYnMuY28wWTATBgcqhkjOPQIBBggqhkjOPQMB
BwNCAAQX3DY0E6KiH8mHKy7TPyJkXLmGUyYtFWSIeItWOLR4dZkRCAfWV5gOwZMT
Q3G5+4vyzhWJBHWVK7d5fDAJLMZWo20wazAOBgNVHQ8BAf8EBAMCAaYwHQYDVR0l
BBYwFAYIKwYBBQUHAwIGCCsGAQUFBwMBMA8GA1UdEwEB/wQFMAMBAf8wKQYDVR0O
BCIEIN7Ys1KmUjqzroWnnOzz99/VjGfWDttpXugaCBEWRKihMAoGCCqGSM49BAMC
A0gAMEUCIQC5tsdZFYcL3owgs3MpbnSY6qA60xsxoXSdRaMu0NnoZgIgDPaYYVM4
1gSPt0Z8tUofMix9ITFHCqxrduwHmYQuULc=
-----END CERTIFICATE-----
EOF
~~~

> Agora vamos gerar os hash e comparar o resultado
~~~sh
$ openssl pkey -in minha-chave-privada.key -pubout -outform pem | sha256sum

# Resultado será:
a7936ac08ea74fc98fe906ee621450f352cf9b5ab33e186e1ab48fac505e39a0  -

$ openssl x509 -in meu-certificado.pem -pubkey -noout -outform pem | sha256sum

# Resultado será:
a7936ac08ea74fc98fe906ee621450f352cf9b5ab33e186e1ab48fac505e39a0  -
~~~