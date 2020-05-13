# Trabalhando com certificados

## Gerar certificado

### Certificado
Neste exemplo será apresentado como gerar um certificado e enviar para autoridade Autoridade Certificadora(Certificate Autorithy) ou "Cartório digital" para que seja assinado pela mesma.

* Primeiro precisamos gerar a chave privada (Private Key)
~~~sh
$ openssl genrsa -des3 1024 > ~/chave/minha-chave-privada.key
~~~

* Segundo, precisamos gerar a chave púplica (Public Key).
A emissão do certificado consiste na geração da chave pública também chamada como requisição (request). A chave pública deve conter os  dados de emissor [cidade, estado, nome (common name), email e etc.].

A chave pública deve ser envaida Autoridade Certificadora para que seja criado um "certificado".

~~~sh
$ openssl req -new -key ~/chave/minha-chave-privada.key > ~/chave/minha-solicitacao-deusimar.csr
~~~

> Dados a serem preeenchidos
~~~txt
-----
Country Name (2 letter code) [AU]:BR
State or Province Name (full name) [Some-State]:Distrito Federal
Locality Name (eg, city) []:Brasilia
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Villa Labs Serviços Digitais
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:Deusimar Ferreira dos Anjos
Email Address []:deusimar.anjos@gmail.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:exemplogit
An optional company name []:
~~~

> Sintése
~~~txt
~/chave/minha-chave-privada.key ==> chave privada protegido por uma senha. Nunca deve ser compartilhada, enviada ou entregue a alguém, principalmente a senha que abre esse arquivo.

~/chave/minha-solicitacao-deusimar.csr ==> a chave pública, gerada apartir de uma chave privada, contém seus dados. Esse arquivo é o que você envia a Autoridade Certificadora.
~~~

~~~txt
O  seu  certificado  nesta  atividade  deverá  ser  assinado  pelo  cartório digital  que  você  criou  na  parte  I.  Para  entender  melhor  como proceder, assista ao vídeo disponível no Youtube.-XCA -Vídeo 3 -Colocando o cartório para funcionarhttps://www.youtube.com/watch?v=2D2b9Pbl1UI
~~~

### Auto-assinado

## Importando Certificado
~~~bash
echo | openssl s_client -showcerts -servername hod -connect hod.serpro.gov.br:443 2>/dev/null | awk '/-----BEGIN CERTIFICATE-----/, /-----END CERTIFICATE-----/' >> ?

# Red Hat
/usr/share/pki/ca-trust-source/anchors/hod.crt
update-ca-trust

# Ubuntu
/usr/local/share/ca-certificates/hod.crt
~~~

## Verificando Certificado e Chave
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

[Cadeia de certificado ICP-Brasil](https://blog.certisign.com.br/certificado-digital-ssl-invalido-ou-nao-confiavel-na-rfb/)
