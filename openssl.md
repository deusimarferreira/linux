# Trabalhando com certificados

## # Importando Certificado
~~~bash
echo | openssl s_client -showcerts -servername hod -connect hod.serpro.gov.br:443 2>/dev/null | awk '/-----BEGIN CERTIFICATE-----/, /-----END CERTIFICATE-----/' >> /usr/local/share/ca-certificates/hod/ca-certificates.crt
