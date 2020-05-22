# Uso do comando find

~~~sh
find ./ -name "libssl"
~~~

> Usando o retorno do find e remover
~~~sh
rm -rf $(find ./ -name "__pycache__")
~~~
