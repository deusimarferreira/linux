# Trabalhando com certificados

## Importando Certificado
~~~bash
echo | openssl s_client -showcerts -servername hod -connect hod.serpro.gov.br:443 2>/dev/null | awk '/-----BEGIN CERTIFICATE-----/, /-----END CERTIFICATE-----/' >> ?

# Red Hat
/usr/share/pki/ca-trust-source/anchors/hod.crt
update-ca-trust

# Ubuntu
/usr/local/share/ca-certificates/hod.crt
~~~

[Cadeia de certificado ICP-Brasil](https://blog.certisign.com.br/certificado-digital-ssl-invalido-ou-nao-confiavel-na-rfb/)
