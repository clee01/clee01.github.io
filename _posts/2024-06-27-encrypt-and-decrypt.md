# Files encryptor and decryptor(plateform: Windows10)

## 0x00 Install mingw64

### Download mingw-builds-binaries
[download-link](https://github.com/niXman/mingw-builds-binaries/releases)
![image](https://github.com/clee01/clee01.github.io/assets/34154239/53da4a2d-9f36-49f4-a58d-ec1a7a5a1322)


### Unzip to a custom folder
```
# My custom folder
PS C:\mingw64> pwd

Path
----
C:\mingw64
```

### Add mingw bin to system PATH
`C:\mingw64\bin`
![image](https://github.com/clee01/clee01.github.io/assets/34154239/0e8e1f9a-77e5-4b7c-b7c5-3ee6493c1805)

### Check whether its installed
```
PS C:\> g++ --version
g++.exe (x86_64-win32-seh-rev0, Built by MinGW-Builds project) 13.2.0
Copyright (C) 2023 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

## 0x01 Install OpenSSL

### Download OpenSSL
[download-link](https://slproweb.com/products/Win32OpenSSL.html)
![image](https://github.com/clee01/clee01.github.io/assets/34154239/c5515967-1da3-4efb-a7c3-08d77815e281)

### Install step by step as followed by `Win64OpenSSL-3_0_14.exe`

### Add OpenSSL bin to system PATH
![image](https://github.com/clee01/clee01.github.io/assets/34154239/f531ade5-4124-4781-857f-0a718ccea260)

### Check whether its installed
```
PS C:\> openssl version
OpenSSL 3.0.14 4 Jun 2024 (Library: OpenSSL 3.0.14 4 Jun 2024)
```

## 0x02 Install libcurl

### Download libcurl
[download-link](https://curl.se/windows/)
![image](https://github.com/clee01/clee01.github.io/assets/34154239/06b6a87f-52e0-4187-91d2-6d71af905daa)

### Unzip to a custom folder
```
# My custom folder
PS D:\curl-8.8.0_2-win64-mingw> pwd

Path
----
D:\curl-8.8.0_2-win64-mingw
```

### Add libcurl bin to system PATH
![image](https://github.com/clee01/clee01.github.io/assets/34154239/67b6800a-177d-4f69-8c3d-5cbadd57c52b)

### Check whether its installed
```
PS D:\curl-8.8.0_2-win64-mingw\bin> .\curl.exe --version
curl 8.8.0 (x86_64-w64-mingw32) libcurl/8.8.0 LibreSSL/3.9.2 zlib/1.3.1 brotli/1.1.0 zstd/1.5.6 WinIDN libpsl/0.21.5 libssh2/1.11.0 nghttp2/1.62.1 ngtcp2/1.6.0 nghttp3/1.4.0
Release-Date: 2024-05-22
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns ldap ldaps mqtt pop3 pop3s rtsp scp sftp smb smbs smtp smtps telnet tftp ws wss
Features: alt-svc AsynchDNS brotli HSTS HTTP2 HTTP3 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM PSL SPNEGO SSL SSPI threadsafe UnixSockets zstd
```

## 0x03 Install php

### Download php
[download-link](https://windows.php.net/download/)

### Unzip to a custom folder
```
PS D:\php> pwd

Path
----
D:\php
```

### Add php bin to system PATH
![image](https://github.com/clee01/clee01.github.io/assets/34154239/297e52fb-04ee-4d5c-b83f-99775107c247)

### Add `php.ini` file
```
PS D:\php> cp .\php.ini-development php.ini
PS D:\php> vim php.ini

# Needs to be adjusted
...
; On windows:
extension_dir = "D:\php\ext"
...
extension=openssl
...
```

### Check whether its installed
```
PS C:\> php -v
PHP 8.3.8 (cli) (built: Jun  4 2024 18:52:30) (ZTS Visual C++ 2019 x64)
Copyright (c) The PHP Group
Zend Engine v4.3.8, Copyright (c) Zend Technologies
```

## 0x04 Codes
### Directory structure
```
PS C:\encrypt_and_decrypt> dir


    目录: C:\encrypt_and_decrypt


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         2024/6/27     16:32                files               # Directory for encrypted and decrypted
-a----         2024/6/27     11:36            160 config.ini          # Configuration file
-a----         2024/6/27     11:10           2761 decryptor.php       # Webserver: decrypt files in directory
-a----         2024/6/27     16:32           2694 decrypt_helper.cpp  # Send key to webserver
-a----         2024/6/27     16:32          90405 decrypt_helper.exe  # Send key to webserver
-a----         2024/6/27     11:34           5742 encryptor.cpp       # Encrypt files in directory
-a----         2024/6/27     10:30         148829 encryptor.exe       # Encrypt files in directory
```

### Run the webserver
```
PS C:\encrypt_and_decrypt> php -S localhost:8000
[Thu Jun 27 17:28:33 2024] PHP 8.3.8 Development Server (http://localhost:8000) started
```

### Compile encryptor.cpp and run
```
PS C:\encrypt_and_decrypt> g++ -o encryptor encryptor.cpp -IC:\OpenSSL-Win64\include -LC:\OpenSSL-Win64\lib\VC\x64\MD  -lssl -lcrypto -std=c++17
PS C:\encrypt_and_decrypt> .\encryptor.exe
Encrypting files in directory: C:\encrypt_and_decrypt\files
Encrypting file: C:\encrypt_and_decrypt\files\1.txt
Encrypting file: C:\encrypt_and_decrypt\files\2.txt
Encrypting file: C:\encrypt_and_decrypt\files\nested\3.txt
Encryption completed.
```
![image](https://github.com/clee01/clee01.github.io/assets/34154239/c0f59ec8-6a61-46fc-b03c-de7b460c737f)

### Compile decrypt_helper.cpp and run
```
PS C:\encrypt_and_decrypt> g++ -o .\decrypt_helper .\decrypt_helper.cpp  -I"D:\curl-8.8.0_2-win64-mingw\include" -L"D:\curl-8.8.0_2-win64-mingw\lib" -lcurl
PS C:\encrypt_and_decrypt> .\decrypt_helper.exe
{"status":"success","message":"Files decrypted successfully"}Request sent successfully!
```
![image](https://github.com/clee01/clee01.github.io/assets/34154239/4c4b0886-f4cc-44d5-aed1-3b65e9fce87a)
![image](https://github.com/clee01/clee01.github.io/assets/34154239/4354a949-6b72-494c-a108-24d817895762)
