# Gerar Certificado

## Certificado
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

## Auto-assinado