# kubectl-show-tls

Show decoded TLS secret and verify for consistency:

- Decode all certificates in the chain
- Check for key validity (RSA only for now)
- Check certificate chain validity
- Checks if certificate matches the key (RSA only for now)

Accepts only secrets with `spec.type=kubernetes.io/tls`.

# Install

First be sure you have following commands installed:

- jq: https://jqlang.github.io/jq/
- openssl: check your distro for the package.
- awk: check your distro for the package.

Copy both files to your PATH:

```
$ sudo install --mode=755 kubectl-show_tls /usr/local/bin
$ sudo install --mode=744 kubectl-show_tls.awk /usr/local/bin
```

# Usage

```
$ kubectl get secret wildcard-tls
NAME           TYPE                DATA   AGE
wildcard-tls   kubernetes.io/tls   2      308d

+ kubectl show-tls wildcard-tls
----------------------------------------------------------------
Found certificate:
-----BEGIN CERTIFICATE-----
MIIFCDCCA/CgAwIBAgISAyzfsKmqzubYeeDZk7IQKpLEMA0GCSqGSIb3DQEBCwUA
A1UUEFjAUBggrBgEFBQcDAdDwEB/wQEAwIFoDAdBgNVHSQYIKwYBBQUHAwIwDAYD
VR0QUmXg8Bi39cENmijLKsTAQH/BAIwADAdBgNVHQ4EFgmEwKbGjSBIwHwYDVR0j
BBg+vnYsUwsYwVQYIKwYBBwFoAUFC6zF7dYVsuuUAlA5hQUHAQEESTBHMCEGCCsG
AQU5sZW5jci5vcmcwIgYIKFBzABhhVodHRwOi8vcjMubywYBBQUHMAKGFmh0dHA6
Ly9YDVR0RBCIwIIIeyZy8wKQmQuKi5wcyMy5pLmxlbmNyLm9YWx0ZXJkYXRhc29m
dHdQMMAowCAYGZ4EMGA1UdIAIIBAQIBMhcmUuY29tLmJyMBMAwYKKwYBBAHWeQIE
MDIYDVQQKEw1MZXQnTMRYwFAmNycyBFbxCzAJBgNVBAYTAlVeXB0MQswCQYDVQQD
EwJBaFw0yMzEyMjcxxMzU2MDTlaMzU1NSMzAeFw0yMzA5MjgMCkxJzAlBgNVBAMM
HioR3YXJlLmNvbS5i0YXNvZnSIwcjCCAucHJkLmFsdGVyZGFDQYJKoZIhvcNAQEB
BQAoJlUfhpfQ2RNPEBAK5Lpw883Axs9sDggEPADCCAQoCggEP8tKKeRNsNYOShYl
Z5/S6hGks0ce+hQ/XBnEg59XDWMl1JCbbhAenSVlcWh+5+Mpdmr/dszYyLQFaHyg
XFQhYlHwklC7OdBsCjUb0/7SNsJ5yrP7dSLnSM8s9+t4FVlH50mV3OZTqH1VmiA6
kXcTF0aQYsfRUjxHgbRinVO8Y9oA3VufLE0AzSr+Lqul6MW5UpZMiA4yLCScVVFT
puiHEFAIgEg9NvOqJIJ+ajpxfZ6K8QMUhuYRd2XTrSTy5SPsmxpK+w4elpYCMDB0
R2FELBQADggEBACfqIhvcNAQPNFR5xTS1epL6h6cwDQYJKoZknFsi6Uh8IUuR5lN
mOAqKrPYoj9UX//eLYjDJxJt5ZXv0g7apo1wfaqm3UXx50fO0/Oh/Xpz7HIquC1K
MzFJQpYT1+5CCbNLwS7Gk2CZWN43TyCXbUteIE5oLrlIL4iNjuphGDsGLXJJhyBy
geE5xrcpg6TqVV9BKqb2T/DVfRZHDSabpZSo3665TMeLh7iFYAkW7bIPYeEPv3p4
KtdD/H7CN04UcCZajn32GqvIkc+FYX3RsG9etG8xHlCz6ZH97VvgbTJYI+0cOmxU
DekCAqoMdJNQYJj2M0P4dAagN5WdslUEP/H5VFubCXnbiWWwEAOCAh8wggIbMA4G
8QDvAHYAejKMVNi3LbTvSK8AgSYg6jjgUh7phBZwMhOFTB9ASBE6V6NS61IAAAGK
nqH6R/NojiW5scBuzfFHjVv3EoizwAABAMARzBFAiEA88Ch386EWIEytXebM3hoC
ncYWNZPhaV8vS0JIKAHUA6DIE1eRDRZPBE5lP7Fr9ImdoDDcTV7Q2j71BjUy51co
AAAGK3EoivgAABAMARjBEAivIlryQPTy9ERa+zraeF3fW0GvW4BKD/+V2TyHpMGd
ZTy4Ttdf1p3s9Dsg4W/hcjhGAABAhkFqG4+DAnXFVNZVn/sfiFx8oncpp+da/h6J
EJZyTfa2CgCFPLZxYU6By612exz/jWpRM/MmtMJpKjnofx4lRPsBBg3QfEg=
-----END CERTIFICATE-----
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            03:2c:df:b0:a9:aa:ce:e6:d8:79:e0:d9:93:b2:10:2a:92:c4
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, O = Let's Encrypt, CN = R3
        Validity
            Not Before: Sep 28 13:56:00 2023 GMT
            Not After : Dec 27 13:55:59 2023 GMT
        Subject: CN = *.example.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:ae:4b:a7:0a:09:95:47:e1:a5:f4:36:44:d3:c4:
                    85:0f:d7:97:52:42:6c:35:8c:76:6a:ff:76:cc:d8:
                    c8:b4:05:68:7c:a0:5c:54:1d:48:b9:d2:33:cb:3d:
                    64:7f:85:61:7d:d1:b0:6f:5e:b4:6f:31:2a:d7:43:
                    fa:de:05:56:51:e3:51:bd:3f:ed:28:58:94:7c:24:
                    94:2e:ce:74:1b:02:e7:2a:cf:ec:db:09:e7:49:95:
                    dc:e6:53:a8:7d:55:9a:20:3a:91:77:0b:13:40:33:
                    ff:de:d5:aa:fb:e0:6d:32:58:23:ed:1c:3a:6c:54:
                    80:de:6a:a0:c7:49:35:06:09:8f:63:34:3f:87:42:
                    5e:76:e2:59:65:9d:b2:55:04:3f:f1:f9:54:5b:9b:
                    4a:bf:8b:aa:e9:7a:31:6e:5b:46:29:d5:3b:c4:c5:
                    d1:a4:18:b1:f4:54:8f:11:e0:03:75:6e:7d:8f:68:
                    03:1b:3d:b3:cf:37:3f:cb:4a:29:e4:4d:b0:d6:0e:
                    4a:16:25:67:9f:db:84:07:a7:49:59:5c:5a:1f:b9:
                    f8:ca:41:9c:48:39:f5:74:ba:84:69:2c:d1:c7:be:
                    52:96:4c:88:0e:32:2c:24:9c:55:51:53:22:47:07:
                    ec:23:74:e1:47:02:65:a8:e7:df:61:87:94:2c:fa:
                    0d:e9
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage: 
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            X509v3 Subject Key Identifier: 
                99:78:3C:06:2D:FD:70:43:66:8A:32:CA:B2:61:30:29:B1:A3:48:12
            X509v3 Authority Key Identifier: 
                14:2E:B3:17:B7:58:56:CB:AE:50:09:40:E6:1F:AF:9D:8B:14:C2:C6
            Authority Information Access: 
                OCSP - URI:http://r3.o.lencr.org
                CA Issuers - URI:http://r3.i.lencr.org/
            X509v3 Subject Alternative Name: 
                DNS:*.example.com
            X509v3 Certificate Policies: 
                Policy: 2.23.140.1.2.1
            CT Precertificate SCTs: 
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : 7A:32:8C:54:D8:B7:2D:B6:20:EA:38:E0:52:1E:E9:84:
                                16:70:32:13:85:4D:3B:D2:2B:C1:3A:57:A3:52:EB:52
                    Timestamp : Sep 28 14:56:00.719 2023 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:45:02:21:00:F3:C0:A1:DF:CE:A7:A8:7E:91:FC:DA:
                                23:89:6E:6C:70:1B:B3:7C:51:E3:56:F1:16:20:4C:AD:
                                5D:E6:CC:DE:1A:02:20:4D:5E:44:34:59:3C:11:39:94:
                                FE:C5:AF:D2:26:76:80:C3:71:35:67:71:85:8D:64:F8:
                                5A:57:CB:D2:D0:92:0A
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : E8:3E:D0:DA:3E:F5:06:35:32:E7:57:28:BC:89:6B:C9:
                                03:D3:CB:D1:11:6B:EC:EB:69:E1:77:7D:6D:06:BD:6E
                    Timestamp : Sep 28 14:56:00.702 2023 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:44:02:20:4A:0F:FF:95:D9:3C:87:A4:C1:9D:A6:E8:
                                A1:B9:84:5D:D9:74:EB:49:3C:B9:48:FB:08:27:E6:A3:
                                A7:11:C4:14:02:20:12:0F:4D:BC:EA:89:2B:C4:0C:51:
                                F6:7A:9B:1A:4A:FB:0E:1E:96:96:02:30:30:74:47:61:
                                75:7A:92:FA:87:A7
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        27:ea:47:9c:53:48:f3:45:92:71:6c:8b:a5:21:f0:85:2e:47:
        99:4d:b7:96:6b:3d:8a:23:f5:45:ff:fd:e2:d8:8c:32:77:51:
        7c:79:d1:f5:ef:d2:0e:da:a6:8d:70:7d:aa:a6:98:e0:2a:28:
        ed:3f:c4:93:a1:fd:7a:73:ec:72:2a:b8:2d:4a:65:63:69:61:
        3d:7e:e4:20:9b:34:bc:12:ec:69:0b:ae:52:0b:e2:2e:37:4f:
        20:97:6d:4b:5e:20:4e:68:33:31:49:40:d8:ee:d8:2a:61:18:
        3b:06:2d:72:49:87:20:72:55:f4:6b:72:98:3a:4e:a5:55:f4:
        12:aa:6f:64:d3:31:e2:e1:ee:26:47:0d:26:9b:a5:94:a8:df:
        ae:b9:81:e1:39:c4:56:00:fc:39:16:ed:b2:0f:61:e1:0f:bf:
        7a:78:18:00:01:02:19:05:a8:6e:3e:0c:09:d7:15:53:59:56:
        7f:ec:7e:21:59:4f:2e:13:b5:d7:f5:a7:7b:3d:0e:c8:38:5b:
        f8:5c:8e:1c:7c:a2:77:29:a7:e7:5a:fe:1e:89:10:96:72:4d:
        f6:b6:0a:00:85:3c:b6:71:61:4e:81:cb:ad:76:7b:1c:ff:8d:
        6a:51:33:f3:26:b4:c2:69:2a:39:e8:7f:1e:25:44:fb:01:06:
        0d:d0:7c:48
----------------------------------------------------------------
Found certificate:
-----BEGIN CERTIFICATE-----
MIIFFjCCAv6gAwIBAgIRAJErCErPDBinU/bWLiWnX1owDQYJKoZIhvcNAQELBQAw
TzELMAkGA1UEBhMCVVMxKTAnBgNVBAoTIEludGVybmV0IFNlY3VyaXR5IFJlc2Vh
cmNoIEdyb3VwMRUwEwYDVQQDEwxJU1JHIFJvb3QgWDEwHhcNMjAwOTA0MDAwMDAw
WhcNMjUwOTE1MTYwMDAwWjAyMQswCQYDVQQGEwJVUzEWMBQGA1UEChMNTGV0J3Mg
RW5jcnlwdDELMAkGA1UEAxMCUjMwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEK
AoIBAQC7AhUozPaglNMPEuyNVZLD+ILxmaZ6QoinXSaqtSu5xUyxr45r+XXIo9cP
R5QUVTVXjJ6oojkZ9YI8QqlObvU7wy7bjcCwXPNZOOftz2nwWgsbvsCUJCWH+jdx
sxPnHKzhm+/b5DtFUkWWqcFTzjTIUu61ru2P3mBw4qVUq7ZtDpelQDRrK9O8Zutm
NHz6a4uPVymZ+DAXXbpyb/uBxa3Shlg9F8fnCbvxK/eG3MHacV3URuPMrSXBiLxg
Z3Vms/EY96Jc5lP/Ooi2R6X/ExjqmAl3P51T+c8B5fWmcBcUr2Ok/5mzk53cU6cG
/kiFHaFpriV1uxPMUgP17VGhi9sVAgMBAAGjggEIMIIBBDAOBgNVHQ8BAf8EBAMC
AYYwHQYDVR0lBBYwFAYIKwYBBQUHAwIGCCsGAQUFBwMBMBIGA1UdEwEB/wQIMAYB
Af8CAQAwHQYDVR0OBBYEFBQusxe3WFbLrlAJQOYfr52LFMLGMB8GA1UdIwQYMBaA
FHm0WeZ7tuXkAXOACIjIGlj26ZtuMDIGCCsGAQUFBwEBBCYwJDAiBggrBgEFBQcw
AoYWaHR0cDovL3gxLmkubGVuY3Iub3JnLzAnBgNVHR8EIDAeMBygGqAYhhZodHRw
Oi8veDEuYy5sZW5jci5vcmcvMCIGA1UdIAQbMBkwCAYGZ4EMAQIBMA0GCysGAQQB
gt8TAQEBMA0GCSqGSIb3DQEBCwUAA4ICAQCFyk5HPqP3hUSFvNVneLKYY611TR6W
PTNlclQtgaDqw+34IL9fzLdwALduO/ZelN7kIJ+m74uyA+eitRY8kc607TkC53wl
ikfmZW4/RvTZ8M6UK+5UzhK8jCdLuMGYL6KvzXGRSgi3yLgjewQtCPkIVz6D2QQz
CkcheAmCJ8MqyJu5zlzyZMjAvnnAT45tRAxekrsu94sQ4egdRCnbWSDtY7kh+BIm
lJNXoB1lBMEKIq4QDUOXoRgffuDghje1WrG9ML+Hbisq/yFOGwXD9RiX8F6sw6W4
avAuvDszue5L3sz85K+EC4Y/wFVDNvZo4TYXao6Z0f+lQKc0t8DQYzk1OXVu8rp2
yJMC6alLbBfODALZvYH7n7do1AZls4I9d1P4jnkDrQoxB3UqQ9hVl3LEKQ73xF1O
yK5GhDDX8oVfGKF5u+decIsH4YaTw7mP3GFxJSqv3+0lUFJoi5Lc5da149p90Ids
hCExroL1+7mryIkXPeFM5TgO9r0rvZaBFOvV2z0gp35Z0+L4WPlbuEjN/lxPFin+
HlUjr8gRsI3qfJOQFy/9rKIJR0Y/8Omwt/8oTWgy1mdeHmmjk7j1nYsvC9JSQ6Zv
MldlTTKB3zhThV1+XWYp6rjd5JW1zbVWEkLNxE7GJThEUG3szgBVGP7pSWTUTsqX
nLRbwHOoq7hHwg==
-----END CERTIFICATE-----
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            91:2b:08:4a:cf:0c:18:a7:53:f6:d6:2e:25:a7:5f:5a
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, O = Internet Security Research Group, CN = ISRG Root X1
        Validity
            Not Before: Sep  4 00:00:00 2020 GMT
            Not After : Sep 15 16:00:00 2025 GMT
        Subject: C = US, O = Let's Encrypt, CN = R3
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:bb:02:15:28:cc:f6:a0:94:d3:0f:12:ec:8d:55:
                    92:c3:f8:82:f1:99:a6:7a:42:88:a7:5d:26:aa:b5:
                    2b:b9:c5:4c:b1:af:8e:6b:f9:75:c8:a3:d7:0f:47:
                    94:14:55:35:57:8c:9e:a8:a2:39:19:f5:82:3c:42:
                    a9:4e:6e:f5:3b:c3:2e:db:8d:c0:b0:5c:f3:59:38:
                    e7:ed:cf:69:f0:5a:0b:1b:be:c0:94:24:25:87:fa:
                    37:71:b3:13:e7:1c:ac:e1:9b:ef:db:e4:3b:45:52:
                    45:96:a9:c1:53:ce:34:c8:52:ee:b5:ae:ed:8f:de:
                    60:70:e2:a5:54:ab:b6:6d:0e:97:a5:40:34:6b:2b:
                    d3:bc:66:eb:66:34:7c:fa:6b:8b:8f:57:29:99:f8:
                    30:17:5d:ba:72:6f:fb:81:c5:ad:d2:86:58:3d:17:
                    c7:e7:09:bb:f1:2b:f7:86:dc:c1:da:71:5d:d4:46:
                    e3:cc:ad:25:c1:88:bc:60:67:75:66:b3:f1:18:f7:
                    a2:5c:e6:53:ff:3a:88:b6:47:a5:ff:13:18:ea:98:
                    09:77:3f:9d:53:f9:cf:01:e5:f5:a6:70:17:14:af:
                    63:a4:ff:99:b3:93:9d:dc:53:a7:06:fe:48:85:1d:
                    a1:69:ae:25:75:bb:13:cc:52:03:f5:ed:51:a1:8b:
                    db:15
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Key Usage: critical
                Digital Signature, Certificate Sign, CRL Sign
            X509v3 Extended Key Usage: 
                TLS Web Client Authentication, TLS Web Server Authentication
            X509v3 Basic Constraints: critical
                CA:TRUE, pathlen:0
            X509v3 Subject Key Identifier: 
                14:2E:B3:17:B7:58:56:CB:AE:50:09:40:E6:1F:AF:9D:8B:14:C2:C6
            X509v3 Authority Key Identifier: 
                79:B4:59:E6:7B:B6:E5:E4:01:73:80:08:88:C8:1A:58:F6:E9:9B:6E
            Authority Information Access: 
                CA Issuers - URI:http://x1.i.lencr.org/
            X509v3 CRL Distribution Points: 
                Full Name:
                  URI:http://x1.c.lencr.org/
            X509v3 Certificate Policies: 
                Policy: 2.23.140.1.2.1
                Policy: 1.3.6.1.4.1.44947.1.1.1
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        85:ca:4e:47:3e:a3:f7:85:44:85:bc:d5:67:78:b2:98:63:ad:
        75:4d:1e:96:3d:33:65:72:54:2d:81:a0:ea:c3:ed:f8:20:bf:
        5f:cc:b7:70:00:b7:6e:3b:f6:5e:94:de:e4:20:9f:a6:ef:8b:
        b2:03:e7:a2:b5:16:3c:91:ce:b4:ed:39:02:e7:7c:25:8a:47:
        e6:65:6e:3f:46:f4:d9:f0:ce:94:2b:ee:54:ce:12:bc:8c:27:
        4b:b8:c1:98:2f:a2:af:cd:71:91:4a:08:b7:c8:b8:23:7b:04:
        2d:08:f9:08:57:3e:83:d9:04:33:0a:47:21:78:09:82:27:c3:
        2a:c8:9b:b9:ce:5c:f2:64:c8:c0:be:79:c0:4f:8e:6d:44:0c:
        5e:92:bb:2e:f7:8b:10:e1:e8:1d:44:29:db:59:20:ed:63:b9:
        21:f8:12:26:94:93:57:a0:1d:65:04:c1:0a:22:ae:10:0d:43:
        97:a1:18:1f:7e:e0:e0:86:37:b5:5a:b1:bd:30:bf:87:6e:2b:
        2a:ff:21:4e:1b:05:c3:f5:18:97:f0:5e:ac:c3:a5:b8:6a:f0:
        2e:bc:3b:33:b9:ee:4b:de:cc:fc:e4:af:84:0b:86:3f:c0:55:
        43:36:f6:68:e1:36:17:6a:8e:99:d1:ff:a5:40:a7:34:b7:c0:
        d0:63:39:35:39:75:6e:f2:ba:76:c8:93:02:e9:a9:4b:6c:17:
        ce:0c:02:d9:bd:81:fb:9f:b7:68:d4:06:65:b3:82:3d:77:53:
        f8:8e:79:03:ad:0a:31:07:75:2a:43:d8:55:97:72:c4:29:0e:
        f7:c4:5d:4e:c8:ae:46:84:30:d7:f2:85:5f:18:a1:79:bb:e7:
        5e:70:8b:07:e1:86:93:c3:b9:8f:dc:61:71:25:2a:af:df:ed:
        25:50:52:68:8b:92:dc:e5:d6:b5:e3:da:7d:d0:87:6c:84:21:
        31:ae:82:f5:fb:b9:ab:c8:89:17:3d:e1:4c:e5:38:0e:f6:bd:
        2b:bd:96:81:14:eb:d5:db:3d:20:a7:7e:59:d3:e2:f8:58:f9:
        5b:b8:48:cd:fe:5c:4f:16:29:fe:1e:55:23:af:c8:11:b0:8d:
        ea:7c:93:90:17:2f:fd:ac:a2:09:47:46:3f:f0:e9:b0:b7:ff:
        28:4d:68:32:d6:67:5e:1e:69:a3:93:b8:f5:9d:8b:2f:0b:d2:
        52:43:a6:6f:32:57:65:4d:32:81:df:38:53:85:5d:7e:5d:66:
        29:ea:b8:dd:e4:95:b5:cd:b5:56:12:42:cd:c4:4e:c6:25:38:
        44:50:6d:ec:ce:00:55:18:fe:e9:49:64:d4:4e:ca:97:9c:b4:
        5b:c0:73:a8:ab:b8:47:c2
----------------------------------------------------------------
Found certificate:
-----BEGIN CERTIFICATE-----
MIIFYDCCBEigAwIBAgIQQAF3ITfU6UK47naqPGQKtzANBgkqhkiG9w0BAQsFADA/
MSQwIgYDVQQKExtEaWdpdGFsIFNpZ25hdHVyZSBUcnVzdCBDby4xFzAVBgNVBAMT
DkRTVCBSb290IENBIFgzMB4XDTIxMDEyMDE5MTQwM1oXDTI0MDkzMDE4MTQwM1ow
TzELMAkGA1UEBhMCVVMxKTAnBgNVBAoTIEludGVybmV0IFNlY3VyaXR5IFJlc2Vh
cmNoIEdyb3VwMRUwEwYDVQQDEwxJU1JHIFJvb3QgWDEwggIiMA0GCSqGSIb3DQEB
AQUAA4ICDwAwggIKAoICAQCt6CRz9BQ385ueK1coHIe+3LffOJCMbjzmV6B493XC
ov71am72AE8o295ohmxEk7axY/0UEmu/H9LqMZshftEzPLpI9d1537O4/xLxIZpL
wYqGcWlKZmZsj348cL+tKSIG8+TA5oCu4kuPt5l+lAOf00eXfJlII1PoOK5PCm+D
LtFJV4yAdLbaL9A4jXsDcCEbdfIwPPqPrt3aY6vrFk/CjhFLfs8L6P+1dy70sntK
4EwSJQxwjQMpoOFTJOwT2e4ZvxCzSow/iaNhUd6shweU9GNx7C7ib1uYgeGJXDR5
bHbvO5BieebbpJovJsXQEOEO3tkQjhb7t/eo98flAgeYjzYIlefiN5YNNnWe+w5y
sR2bvAP5SQXYgd0FtCrWQemsAXaVCg/Y39W9Eh81LygXbNKYwagJZHduRze6zqxZ
Xmidf3LWicUGQSk+WT7dJvUkyRGnWqNMQB9GoZm1pzpRboY7nn1ypxIFeFntPlF4
FQsDj43QLwWyPntKHEtzBRL8xurgUBN8Q5N0s8p0544fAQjQMNRbcTa0B7rBMDBc
SLeCO5imfWCKoqMpgsy6vYMEG6KDA0Gh1gXxG8K28Kh8hjtGqEgqiNx2mna/H2ql
PRmP6zjzZN7IKw0KKP/32+IVQtQi0Cdd4Xn+GOdwiK1O5tmLOsbdJ1Fu/7xk9TND
TwIDAQABo4IBRjCCAUIwDwYDVR0TAQH/BAUwAwEB/zAOBgNVHQ8BAf8EBAMCAQYw
SwYIKwYBBQUHAQEEPzA9MDsGCCsGAQUFBzAChi9odHRwOi8vYXBwcy5pZGVudHJ1
c3QuY29tL3Jvb3RzL2RzdHJvb3RjYXgzLnA3YzAfBgNVHSMEGDAWgBTEp7Gkeyxx
+tvhS5B1/8QVYIWJEDBUBgNVHSAETTBLMAgGBmeBDAECATA/BgsrBgEEAYLfEwEB
ATAwMC4GCCsGAQUFBwIBFiJodHRwOi8vY3BzLnJvb3QteDEubGV0c2VuY3J5cHQu
b3JnMDwGA1UdHwQ1MDMwMaAvoC2GK2h0dHA6Ly9jcmwuaWRlbnRydXN0LmNvbS9E
U1RST09UQ0FYM0NSTC5jcmwwHQYDVR0OBBYEFHm0WeZ7tuXkAXOACIjIGlj26Ztu
MA0GCSqGSIb3DQEBCwUAA4IBAQAKcwBslm7/DlLQrt2M51oGrS+o44+/yQoDFVDC
5WxCu2+b9LRPwkSICHXM6webFGJueN7sJ7o5XPWioW5WlHAQU7G75K/QosMrAdSW
9MUgNTP52GE24HGNtLi1qoJFlcDyqSMo59ahy2cI2qBDLKobkx/J3vWraV0T9VuG
WCLKTVXkcGdtwlfFRjlBz4pYg1htmf5X6DYO8A4jqv2Il9DjXA6USbW1FzXSLr9O
he8Y4IWS6wY7bCkjCWDcRQJMEhg76fsO3txE+FiYruq9RUWhiF1myv4Q6W+CyBFC
Dfvp7OOGAN6dEOM4+qR9sdjoSYKEBpsr6GtPAQw4dy753ec5
-----END CERTIFICATE-----
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            40:01:77:21:37:d4:e9:42:b8:ee:76:aa:3c:64:0a:b7
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: O = Digital Signature Trust Co., CN = DST Root CA X3
        Validity
            Not Before: Jan 20 19:14:03 2021 GMT
            Not After : Sep 30 18:14:03 2024 GMT
        Subject: C = US, O = Internet Security Research Group, CN = ISRG Root X1
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (4096 bit)
                Modulus:
                    00:ad:e8:24:73:f4:14:37:f3:9b:9e:2b:57:28:1c:
                    87:be:dc:b7:df:38:90:8c:6e:3c:e6:57:a0:78:f7:
                    75:c2:a2:fe:f5:6a:6e:f6:00:4f:28:db:de:68:86:
                    6c:44:93:b6:b1:63:fd:14:12:6b:bf:1f:d2:ea:31:
                    9b:21:7e:d1:33:3c:ba:48:f5:dd:79:df:b3:b8:ff:
                    12:f1:21:9a:4b:c1:8a:86:71:69:4a:66:66:6c:8f:
                    7e:3c:70:bf:ad:29:22:06:f3:e4:c0:e6:80:ae:e2:
                    4b:8f:b7:99:7e:94:03:9f:d3:47:97:7c:99:48:23:
                    53:e8:38:ae:4f:0a:6f:83:2e:d1:49:57:8c:80:74:
                    b6:da:2f:d0:38:8d:7b:03:70:21:1b:75:f2:30:3c:
                    fa:8f:ae:dd:da:63:ab:eb:16:4f:c2:8e:11:4b:7e:
                    cf:0b:e8:ff:b5:77:2e:f4:b2:7b:4a:e0:4c:12:25:
                    0c:70:8d:03:29:a0:e1:53:24:ec:13:d9:ee:19:bf:
                    10:b3:4a:8c:3f:89:a3:61:51:de:ac:87:07:94:f4:
                    63:71:ec:2e:e2:6f:5b:98:81:e1:89:5c:34:79:6c:
                    76:ef:3b:90:62:79:e6:db:a4:9a:2f:26:c5:d0:10:
                    e1:0e:de:d9:10:8e:16:fb:b7:f7:a8:f7:c7:e5:02:
                    07:98:8f:36:08:95:e7:e2:37:96:0d:36:75:9e:fb:
                    0e:72:b1:1d:9b:bc:03:f9:49:05:d8:81:dd:05:b4:
                    2a:d6:41:e9:ac:01:76:95:0a:0f:d8:df:d5:bd:12:
                    1f:35:2f:28:17:6c:d2:98:c1:a8:09:64:77:6e:47:
                    37:ba:ce:ac:59:5e:68:9d:7f:72:d6:89:c5:06:41:
                    29:3e:59:3e:dd:26:f5:24:c9:11:a7:5a:a3:4c:40:
                    1f:46:a1:99:b5:a7:3a:51:6e:86:3b:9e:7d:72:a7:
                    12:05:78:59:ed:3e:51:78:15:0b:03:8f:8d:d0:2f:
                    05:b2:3e:7b:4a:1c:4b:73:05:12:fc:c6:ea:e0:50:
                    13:7c:43:93:74:b3:ca:74:e7:8e:1f:01:08:d0:30:
                    d4:5b:71:36:b4:07:ba:c1:30:30:5c:48:b7:82:3b:
                    98:a6:7d:60:8a:a2:a3:29:82:cc:ba:bd:83:04:1b:
                    a2:83:03:41:a1:d6:05:f1:1b:c2:b6:f0:a8:7c:86:
                    3b:46:a8:48:2a:88:dc:76:9a:76:bf:1f:6a:a5:3d:
                    19:8f:eb:38:f3:64:de:c8:2b:0d:0a:28:ff:f7:db:
                    e2:15:42:d4:22:d0:27:5d:e1:79:fe:18:e7:70:88:
                    ad:4e:e6:d9:8b:3a:c6:dd:27:51:6e:ff:bc:64:f5:
                    33:43:4f
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Basic Constraints: critical
                CA:TRUE
            X509v3 Key Usage: critical
                Certificate Sign, CRL Sign
            Authority Information Access: 
                CA Issuers - URI:http://apps.identrust.com/roots/dstrootcax3.p7c
            X509v3 Authority Key Identifier: 
                C4:A7:B1:A4:7B:2C:71:FA:DB:E1:4B:90:75:FF:C4:15:60:85:89:10
            X509v3 Certificate Policies: 
                Policy: 2.23.140.1.2.1
                Policy: 1.3.6.1.4.1.44947.1.1.1
                  CPS: http://cps.root-x1.letsencrypt.org
            X509v3 CRL Distribution Points: 
                Full Name:
                  URI:http://crl.identrust.com/DSTROOTCAX3CRL.crl
            X509v3 Subject Key Identifier: 
                79:B4:59:E6:7B:B6:E5:E4:01:73:80:08:88:C8:1A:58:F6:E9:9B:6E
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        0a:73:00:6c:96:6e:ff:0e:52:d0:ae:dd:8c:e7:5a:06:ad:2f:
        a8:e3:8f:bf:c9:0a:03:15:50:c2:e5:6c:42:bb:6f:9b:f4:b4:
        4f:c2:44:88:08:75:cc:eb:07:9b:14:62:6e:78:de:ec:27:ba:
        39:5c:f5:a2:a1:6e:56:94:70:10:53:b1:bb:e4:af:d0:a2:c3:
        2b:01:d4:96:f4:c5:20:35:33:f9:d8:61:36:e0:71:8d:b4:b8:
        b5:aa:82:45:95:c0:f2:a9:23:28:e7:d6:a1:cb:67:08:da:a0:
        43:2c:aa:1b:93:1f:c9:de:f5:ab:69:5d:13:f5:5b:86:58:22:
        ca:4d:55:e4:70:67:6d:c2:57:c5:46:39:41:cf:8a:58:83:58:
        6d:99:fe:57:e8:36:0e:f0:0e:23:aa:fd:88:97:d0:e3:5c:0e:
        94:49:b5:b5:17:35:d2:2e:bf:4e:85:ef:18:e0:85:92:eb:06:
        3b:6c:29:23:09:60:dc:45:02:4c:12:18:3b:e9:fb:0e:de:dc:
        44:f8:58:98:ae:ea:bd:45:45:a1:88:5d:66:ca:fe:10:e9:6f:
        82:c8:11:42:0d:fb:e9:ec:e3:86:00:de:9d:10:e3:38:fa:a4:
        7d:b1:d8:e8:49:82:84:06:9b:2b:e8:6b:4f:01:0c:38:77:2e:
        f9:dd:e7:39
----------------------------------------------------------------
Found RSA key:
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEArkunCgmVR+Gl9DZE08QDGz2zzzc/y0op5E2w1g5KFiVnn9uE
udIzyz363gVWUeNRvT/tKFiUfCSULs50GwLnKs/s2wnnSZXc5lOofVWaIDqRdwsT
xbltGKdU7xMXRpBix9FSPEeADdW59j2hSlkyIDjIsJJxVUVMiRwfsQDNKv4uq6Xo
fYYeULPpkf4VhfdGwb160bzEq10P/3tWq++BtMlgj7Rw6bFSA3mqgI3ThRwJlqOf
QIDAQABAoIBAQClnhlxfj2zQ/h0JeduJZZZ2yVQQ/8flUW5stegs5x0k1BgmPYN6
WU3VnwE3bA8cC/SqdBFRN6p3Pbw5dW3GHERPRsu5PMOfQjMRBGieUjT/FgeH5xei
JlOrOxuf9/QHBMVo2L1DYap6UG46CiZEXgX7lIKZyleZlvxX6l/9+h8LklNWjQWD
Rx7B6dJWVxaHXUkJsNYx2av92zNjItAVofKB7n4ykGc6FD9ecVB1ISDn1dLqEaSz
nhioorNB+slUXRd8nSPjX1D1wbplyV4fd7GqUIduMFf2ifzw0+zAAuNmYuzHFNsw
C694ED8h9Hw/xaij/VQVv96KxdUr0NbL0k0lTJcsWat9ag2f3mBFMufYkyJc8GV5
gfMzIa2j9bA7w52slAoGAU2x3JDz1zb/KEObuVfQJ6/It5xfHvWA8wptkbUOXecV
ENJruJl/RTOnsVyyZTSR0CAZ3waSbTBsZl0u8jZ6NZoj9OibolwafK3sFggvFUmj
qrAFDcm/6eJHkh2tqI9byC8sWnB4aDDXIYzE7m91nUWPq8xNb2o+yqOAlrWGNYj/
zpczFlOUPn/IeexFpSNfZIUqU79YQbBCOjQYZPGpChuTTgFYWi2tiE3djo5iFoVU
KpitWi6Vkp0ahk99nQRgzuQst1Hy3bbaaSfSYIXEVGYjBsOMw/80VlYyuAZcgrcD
xTdhxbsO4yhAlQzzdQN6rnd8gwA255aXx/MmoGBAN7kkyRhqS7DygkWkRCx9WQby
3BU3kqKOlIlYP5lrt8Twialnuf75yDqXp1zD5K52Mi+xrT3vTX0Z2Rz3XPo3b2Cg
eLZvLRejTyli8SaqFFoUo/5G9PxmiKd51AoGonWYKafAYBA4BAMgvRGIHOU+Of1u
LmhL6JH8hGfiauynfUMV04DKHPDaYswbbn0oQYI0/sDY0IF12nR4TkxgxYxTocGJ
wQXjOVxqPnxCNvkc9bCFEUGqLUCgYAvU6iJT0UVkYgNvAYWtOcIhumyyynYe7IoH
I9jSbMSFS+9XwJaL8q2haddqbKhEwRWRhCwjIN3yOezZxKJUnOvjybmKqicv7O3s
8HuLAsTIjpxjKUZG6dFTzMa2eOwbMvQ2z1HZAXhmb9hW1Gjikl8GYDwHyBhf2MOn
6YCw91q+R5I1Lt0WWE2QKBgQDKS2At9CvhdFrrCdBQcNdiTQnS0bG7+KMRFSUd94
3EolSVSP5X466oIzqJt83n3SwKyFDvaSKNAh7Umm5k7fhG2Luk+2d/WO3zh3BphZ
CRqemutZCI9wmthV1JTJu9+2g58JGTofhJW08dCwqcNR74MMFTy7wQ==
-----END RSA PRIVATE KEY-----
RSA key ok
----------------------------------------------------------------
Checking chain for 3 certs: SUCCESS
SUCCESS: SHA1 Fingerprint=A3:F2:85:DE:68:D6:B4:6E:AD:36:65:67:07:8A:0B:E1:BD:9D:99:CB is signed by SHA1 Fingerprint=A0:53:48:78:37:5B:FE:84:E8:B7:2C:7C:EE:15:82:7A:6A:F5:A4:05
SUCCESS: SHA1 Fingerprint=A0:53:48:78:37:5B:FE:84:E8:B7:2C:7C:EE:15:82:7A:6A:F5:A4:05 is signed by SHA1 Fingerprint=93:3C:A4:0F:6D:DE:E9:5C:9C:41:9F:50:49:3D:82:BE:03:AD:87:BF
----------------------------------------------------------------
Checking if certificate matches the key: SUCCESS
Certificate modulus: MD5(stdin)= 142c0912b170b7527b3f87dcf7e393bd
Key modulus:         MD5(stdin)= 142c0912b170b7527b3f87dcf7e393bd
```
