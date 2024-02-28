VAMOS LÁ...

Primeiramente o padrão.
```bash
sudo apt update
```

Depois faça uma conta no oracle.com/br

Vá para o menu recursos e baixe o oracle-database 21c.



O arquivo disponível é de formato .rpm, portanto irá precisar de outro programa para converter o .rpm para .deb



INSTALANDO O ALIEN
```bash
sudo apt-get install alien libaio1 unixodbc
```

Em seguida, faça a conversão do arquivo rpm para debian com o seguinte comando:
```bash
sudo alien --scripts -d oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm
```

SE E SOMENTE SE tiver problemas de criação de diretório, faça os seguintes comandos:
```bash
mkdir /tmp/oracle_tmp
mv oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm /tmp/oracle_tmp
cd /tmp/oracle_tmp
sudo alien --scripts -d oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm
```

Se tiver erro ou aviso tipo:

warning: oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID ec551f03: NOKEY


Coloque esse código no terminal:
```bash
wget https://yum.oracle.com/RPM-GPG-KEY-oracle-ol7 -O RPM-GPG-KEY-oracle-ol7
sudo rpm --import RPM-GPG-KEY-oracle-ol7
```

Seguido de:
```bash
sudo alien --to-deb --scripts oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm
```

Isso irá terminar com a frase de aviso (warning) de falta de chave pública e verificar a assinatura do pacote RPM,



Após pedir para o alien converter seu arquivo rpm para debian. Não se preocupe se demorar mais de 1 hora para fazer o processo. É um arquivo de 2GB, vai demorar mesmo.



Então... Tome uma água ou um café.



INSTALANDO O ORACLE DATABASE

Feita a a conversão para debian... Hora de instalar nosso malvado:
```bash
sudo dpkg -i oracle-database-xe-21c_1.0-2_amd64.deb
```

Até ai, tudo ok... Não?

Rode o cat para descobrir exatamente qual o erro pode estar acontecendo.,,
```bash
sudo cat /opt/oracle/cfgtoollogs/netca/netca_configure_out.log
```

Se nenhum erro ocorreu. Você já tem seu oracle database instalado...Vamos configurar:
```bash
sudo /etc/init.d/oracle-xe-21c configure
sudo /etc/init.d/oracle-xe-21c restart
```

Vamos adicionar as variáveis de ambiente:
```bash
echo 'export ORACLE_HOME=/opt/oracle/product/21c/dbhomeXE' >> ~/.bashrc
echo 'export PATH=$PATH:$ORACLE_HOME/bin' >> ~/.bashrc
echo 'export ORACLE_SID=XE' >> ~/.bashrc
source ~/.bashrc
```

Tudo ok? Dê mais um update na sua máquina.

E depois:
```bash
sudo apt-get install openjdk-11-jdk
```

Agora extraia o arquivo SQL Developer baixado e o mova para a pasta desejada. E novamente

converta o arquivo rpm para deb.
```bash
sudo alien --scripts --to-deb sqldeveloper-23.1.1-345.2114.noarch.rpm
```
Lembre-se que a conversão pode demorar um pouco, mas com certeza bem menos que o arquivo anterior.



Em seguida só instalar:
```bash
sudo dpkg -i sqldeveloper_23.1.1-346.2114_all.deb
```

Agora só rodar o comando sqldeveloper e ser feliz!
```bash
sqldeveloper
```

Se chegou até aqui, está completo seu guia de instalação do database e do sqldeveloper da oracle.
