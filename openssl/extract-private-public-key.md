# Extraíndo Chave Privada
Nesse exemplo será demonstrado como extrair a chave privada de um arquivo ``pfx`` e seu hash que será usado para validação do certificado comparando o hash da chave privada com o hash da chave pública. 

> O arquivo ``pfx`` deve estar em formato PKCS#12 e incluir o certificado e a chave privada.

## Extraíndo Chave Pública

~~~sh
# Esse comando extrai a chave privada e palavra passe (senha/password)
$ openssl.exe pkcs12 -in server.pfx -nocerts -out key.pem -nodes

# Esse comando extrai somente a chave privada
$ openssl rsa -in key.pem -out minha-chave-privada.key
~~~

## Extraíndo Certificado ``pem``

~~~sh
$ openssl pkcs12 -in server.pfx -nokeys -out meu-certificado.pem
~~~

## Comparando HASH
Agora vamos gerar os hash e comparar o resultado

~~~sh
$ openssl pkey -in minha-chave-privada.key -pubout -outform pem | sha256sum

# Resultado será:
a7936ac08ea74fc98fe906ee621450f352cf9b5ab33e186e1ab48fac505e39a0  -

$ openssl x509 -in meu-certificado.pem -pubkey -noout -outform pem | sha256sum

# Resultado será:
a7936ac08ea74fc98fe906ee621450f352cf9b5ab33e186e1ab48fac505e39a0  -
~~~

> No exemplo acima o hash da chave privada é exatamente ao hash da chave pública do certificado, assim podemos considerar que as chaves são pares.
