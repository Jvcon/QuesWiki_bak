# TiddlyWiki

## 安装环境

```
$ apt-get install nodejs nginx openssl openssl-devel htpasswd
$ npm install -g tiddlywiki
$ npm install -g pm2
```

## 初始化TiddlyWiki文件夹

```
$ tiddlywiki mynewwiki --init server
```

## 直接启动

```
$ tiddlywiki mynewwiki --listen
```
## 自签发SSL IP证书
1. 生成根密钥

```
$ openssl genrsa -out /etc/pki/CA/private/cakey.pem 2048
```

2. 生成根CA证书

```
$ openssl req -new -x509 -days 3650 -key /etc/pki/CA/private/cakey.pem -out  /etc/pki/CA/cacert.pem

You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [CN]:
State or Province Name (full name) []:Beijing
Locality Name (eg, city) [Beijing]:
Organization Name (eg, company) [MX]:
Organizational Unit Name (eg, section) []:note
Common Name (eg, your name or your server's hostname) []:Aliyun, Global Root CA
```

3. 添加信任

```
$ cat /etc/pki/CA/cacert.pem >> /etc/pki/tls/certs/ca-bundle.crt
```
Windows 需要添加根证书至“受信任的根证书颁发机构”，macOS 需要将其导入“钥匙串访问”并选择信任。

4. 创建请求

```
$ openssl genrsa -out /etc/pki/tls/127.0.0.1.key 2048
$ openssl req -new -key /etc/pki/tls/127.0.0.1.key -out /etc/pki/tls/127.0.0.1.csr

You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [CN]:
State or Province Name (full name) []:Beijing
Locality Name (eg, city) [Beijing]:
Organization Name (eg, company) [MX]:
Organizational Unit Name (eg, section) []:note
Common Name (eg, your name or your server's hostname) []:Aliyun, Global Root CA

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```
5. 附加用途

```
$ vim /etc/pki/tls/openssl.cnf 

...
[ v3_req ]
basicConstraints=CA:TRUE
keyUsage = nonRepudiation, digitalSignature, keyEncipherment
subjectAltName=IP:127.0.0.1
extendedKeyUsage = serverAuth,clientAuth
...
```

配置文件中的 IP 地址 127.0.0.1 需要替换为实际 VPS 的公网 IP 地址。

6. 签发证书

```
$ openssl ca -in /etc/pki/tls/127.0.0.1.csr -extensions v3_req -days 365 -out /etc/pki/tls/127.0.0.1.crt

Using configuration from /etc/pki/tls/openssl.cnf
Check that the request matches the signature
Signature ok
Certificate Details:
     Serial Number: 1 (0x1)
     Validity
         Not Before: Mar 12 06:09:00 2019 GMT
         Not After : Mar 11 06:09:00 2020 GMT
     Subject:
         countryName               = CN
         stateOrProvinceName       = Beijing
         organizationName          = MX
         organizationalUnitName    = note
         commonName                = Aliyun, Global Root CA
     X509v3 extensions:
         X509v3 Basic Constraints: 
             CA:TRUE
         X509v3 Key Usage: 
             Digital Signature, Non Repudiation, Key Encipherment
         X509v3 Extended Key Usage: 
             TLS Web Server Authentication, TLS Web Client Authentication
         X509v3 Subject Alternative Name: 
             IP Address:127.0.0.1
Certificate is to be certified until Mar 11 06:09:00 2020 GMT (365 days)
Sign the certificate? [y/n]:y


1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated
```

## 通过pm2启动，配置nginx反向代理
1. 设置用户权限（TiddlyWiki提供）

```
$ vim mynewwiki/myusers.csv
...
username,password
jane,do3
andy,sm1th
roger,m00re
...
```

2. 启动参数

```
$ cd mynewwiki/
$ cp /etc/pki/tls/127.0.0.1.crt .
$ cp /etc/pki/tls/127.0.0.1.key .
$ pm2 start --name mynewwiki /usr/bin/tiddlywiki -- --listen host=172.24.1.12 port=443 credentials=myusers.csv "readers=(authenticated)" writers=roger tls-key=127.0.0.1.key tls-cert=127.0.0.1.crt
```

3. 设置访问密码验证（Nginx提供）
创建密码文件

```
htpasswd -c .passwd admin
```

配置nginx反向代理设置

```
server {
  server_name example.com;
  location / {
    proxy_pass http://127.0.0.1:443;
    auth_basic "password";
    auth_basic_user_file /path/to/.passwd;
  }
}
```