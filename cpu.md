# Verificação de CPU

~~~sh
$ lscpu | grep -i mhz

# CPU - Número lógico da CPU da forma como é usado pelo kernel do Linux.
# CORE - Número lógico do núcleo de processamento.
$ lscpu -e=CPU,CORE

$ cat /proc/cpuinfo | grep -i mhz | uniq
$ cat /proc/cpuinfo | grep -i mhz

$ less /proc/cpuinfo

# htop
$ htop
~~~
