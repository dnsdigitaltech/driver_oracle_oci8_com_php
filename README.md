# COMO INSTALAR O OCI8 NO UBUNTU 18.04, 18.10, 19.04, 19.10 e PHP 5.6, 7.0, 7.1, 7.2, 7.3, 7.4

## INSTALANDO O JAVA
```
$ sudo apt install openjdk-8-jdk
OR
$ sudo apt install openjdk-11-jdk
OR
$ sudo apt install openjdk-13-jdk
OR
$ sudo apt install openjdk-14-jdk
```
## ATUALIZE O UBUNTU
``
$ sudo apt-get update
``
## CONFIRMANDO A INSTALAÇÃO
```
$ java --version
```
## ALTERNANDO ENTRE AS VERSÕES DO JAVA INTALADO
```
$ sudo update-alternatives --config java
$ sudo update-alternatives --config javac
```

## INSTALANDO O PHP 7.4

```
sudo apt-get update
sudo apt -y install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt -y install php7.4
```

## INSTALANDO O MÓDULOS DO PHP 7.4

```
sudo apt-get install libaio1
sudo apt install php7.4-curl php7.4-cli php7.4-cgi php7.4-common php7.4-dev php7.4-fpm php7.4-imap php7.4-gd php7.4-gmp php7.4-json php7.4-ldap php7.4-mbstring php7.4-mysql php7.4-soap php7.4-xml php7.4-xmlrpc php7.4-zip
```

## INSTALANDO E CONFIGURANDO O ORACLE  11 / 12  CLIENT NO PHP 5.6/7.0/7.1/7.2/7.3/.7.4

### 1 - Fazendo download das instâncias ORACLE no link abaixo
** Oracle 11 **

[https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html](https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html)

Arquivos: `instantclient-basic-linux.x64-11.2.0.4.0.zip` e `instantclient-sdk-linux.x64-11.2.0.4.0.zip`

** Oracle 12 **

[https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html](https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html)

Arquivos: `instantclient-basic-linux.x64-11.2.0.4.0.zip` e `instantclient-sdk-linux.x64-11.2.0.4.0.zip`

### 2 - Criando diretório

```
sudo mkdir -p /opt/oracle/
```

### 3 - Movendo a instancia para o diretório criado

```
sudo mv ~/Downloads/instantclient-*.zip /opt/oracle/
```

### 4 - Entrando no diratorio

```
cd /opt/oracle/
```

### 5 - Descompactando as instancias ORACLE

```
sudo unzip instantclient-basic-*-*.zip
sudo unzip instantclient-sdk-*-*.zip
```

** Oracle 11 ** 
### 6 - Renomeando o diretorio instantclient_11_2

```
sudo mv instantclient_11_2 instantclient
```

** Oracle 12 **
### 6 - Renomeando o diretorio instantclient_12_2

```
sudo mv instantclient_12_2 instantclient
```

### 7 - entrando no diretório instantclient 

```
cd instantclient
```

### 8 - Renomenado e criando alguns arquivos simbólicos de configuração

```
sudo ln -s /opt/oracle/instantclient/libclntsh.so.* /opt/oracle/instantclient/libclntsh.so
sudo ln -s /opt/oracle/instantclient/libocci.so.* /opt/oracle/instantclient/libocci.so
sudo ln -s /opt/oracle/instantclient/ /opt/oracle/instantclient/lib
```

** Oracle 11 **
### 9 - criando diretorios 11.2/client dentro de instantclient

```
sudo mkdir -p include/oracle/11.2/
cd include/oracle/11.2/
```

** Oracle 12 **
### 9 - criando diretorios 12.2/client dentro de instantclient

```
sudo mkdir -p include/oracle/12.2/
cd include/oracle/12.2/
```

```
sudo ln -s ../../../sdk/include client
cd -
```

** Oracle 11 **

```
sudo mkdir -p lib/oracle/11.2/client
cd lib/oracle/11.2/client
```

** Oracle12 **

```
sudo mkdir -p lib/oracle/12.2/client
cd lib/oracle/12.2/client
```

```
sudo ln -s ../../../ lib
cd -
```

### 10 - criando arquivo de configuração que irá se referir a um diretório de pesquisa para o cliente instantâneas bibliotecas Oracle, e conectá-lo:

```
echo /opt/oracle/instantclient/ | sudo tee -a /etc/ld.so.conf.d/oracle.conf
sudo ldconfig
```

### 11 - Criando um link simbólico para o php5 equivalentes:

```
sudo ln -s /usr/include/php5 /usr/include/php
sudo ln -s /usr/include/php70 /usr/include/php
sudo ln -s /usr/include/php71 /usr/include/php
sudo ln -s /usr/include/php72 /usr/include/php
sudo ln -s /usr/include/php73 /usr/include/php
sudo ln -s /usr/include/php74 /usr/include/php
```

### 12 - instalando o OCI8

```
pecl install oci8-2.0.8 (para php5)
pecl install oci8 (para php7+)
```

***OBS: se caso der erro execute para ver se está faltando alguma biblioteca do php
phpize***

### 13 - Colocando o caminho para o cliente instantâneo Oracle

```
instantclient,/opt/oracle/instantclient
```

### 14 - Criando uma extensão de arquivo de conexão (verifique o caminho do seu php)

** PHP 5.6 **
```
echo "extension =oci8.so" >> /etc/php/5.6/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/5.6/cli/php.ini
echo "extension =oci8.so" >> /etc/php/5.6/apache2/php.ini
```

** PHP 7.0 **
```
echo "extension =oci8.so" >> /etc/php/7.0/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/7.0/cli/php.ini
echo "extension =oci8.so" >> /etc/php/7.0/apache2/php.ini
```

** PHP 7.1 **
```
echo "extension =oci8.so" >> /etc/php/7.1/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/7.1/cli/php.ini
echo "extension =oci8.so" >> /etc/php/7.1/apache2/php.ini
```

** PHP 7.2 **
```
echo "extension =oci8.so" >> /etc/php/7.2/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/7.2/cli/php.ini
echo "extension =oci8.so" >> /etc/php/7.2/apache2/php.ini
```

** PHP 7.3 **
```
echo "extension =oci8.so" >> /etc/php/7.3/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/7.3/cli/php.ini
echo "extension =oci8.so" >> /etc/php/7.3/apache2/php.ini
```

** PHP 7.4 **
```
echo "extension =oci8.so" >> /etc/php/7.4/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/7.4/cli/php.ini
echo "extension =oci8.so" >> /etc/php/7.4/apache2/php.ini
```

### 15 reinicie

```
sudo shutdown -r now
```
