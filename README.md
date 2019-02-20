#linux_install_cert

This role will install root and intermediate certificates on Debian- or RedHat-based hosts. It has been tested on Ubuntu 16.04, Ubuntu 18.04, and Centos 7.

## Requirements

* Role uses sudo to create system directories and install certificates; <code>ansible_user</code> must be able to sudo to root without a password.

## Role Variables

The variables in this role include:

|parameter|required|default|choices|comments|
|---|---|---|---|---|
|linux_install_cert_certificates|true|A dictionary of fake certificates| |This is a list of dictionaries. Each dictionary has two required keys: <code>name</code> and <code>pem</code>. <code>name</code> is the filename that will be given to the templated certificate. <code>pem</code> is the certificate provided as a pem-encoded string. Since the default is a list of fake certificates, you probably want to change this.|
|linux_install_cert_path|false|<ul><li>/etc/pki/ca-trust/source/anchors</li><li>/usr/local/share/ca-certificates</li>| |Will default to <code>/etc/pki/ca-trust/source/anchors</code> on Debian and <code>/usr/local/share/ca-certificates</code> on Red Hat. You probably don't want to change this unless you know what you are doing.|


## Dependencies

There are no dependencies


## Example Playbook


```yaml
- name: ROLE | Install fake_cert01 and fake_cert02
  hosts: web
  roles:
    - role: ar_linux_root_ca
      linux_install_cert_certificates:
        - name: fake_cert01.crt
          pem: |
            -----BEGIN CERTIFICATE-----
            MIIEAzCCAuugAwIBAgIJALVxQfhBQwlhMA0GCSqGSIb3DQEBCwUAMIGXMQswCQYD
            VQQGEwJVUzELMAkGA1UECAwCTkUxEDAOBgNVBAcMB1JhbHN0b24xFTATBgNVBAoM
            DERpbm9oZWFkIExMQzEWMBQGA1UECwwNZmFrZSBBRiBjZXJ0czEXMBUGA1UEAwwO
            aGFsLmRvbWFpbi5jb20xITAfBgkqhkiG9w0BCQEWEmRlcmVrQGRpbm9oZWFkLmNv
            bTAeFw0xODA3MTcxODQ3MjlaFw0xOTA3MTcxODQ3MjlaMIGXMQswCQYDVQQGEwJV
            UzELMAkGA1UECAwCTkUxEDAOBgNVBAcMB1JhbHN0b24xFTATBgNVBAoMDERpbm9o
            ZWFkIExMQzEWMBQGA1UECwwNZmFrZSBBRiBjZXJ0czEXMBUGA1UEAwwOaGFsLmRv
            bWFpbi5jb20xITAfBgkqhkiG9w0BCQEWEmRlcmVrQGRpbm9oZWFkLmNvbTCCASIw
            DQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAK5jgl4Fnh6oRu1ZIvPe8JoBLnRM
            q7kOI0EsSO3b8nNmWuug1fNFRaokJYhlMEPRFjOx4rBInzoQzvleTwnuciT9H6eR
            xjLpTennnUKfDu8rambO+abNK0GNe3N9Fy0Zls2ryd0C0Kgwbp0phNTRXec4Rf3p
            uuphZU0nutden/7deFm4+o8IuZQA4NYfSBHGgGvY25IJ5abIllWqvJarnzXnVd5u
            VQJvWGWvAcXxjR3KM1A1zxg53XMoOpiJefUIdHFv0CfS2+fmuNYtLgsEutq8WtWP
            LKS1Rbr/mDoi+p0KtDs2Og+exFG9hA/PnxxzYKsX5RnjQsLkHMa2F/639lkCAwEA
            AaNQME4wHQYDVR0OBBYEFIoVrzVXcBcpwlx/IdGUR9rqzYL7MB8GA1UdIwQYMBaA
            FIoVrzVXcBcpwlx/IdGUR9rqzYL7MAwGA1UdEwQFMAMBAf8wDQYJKoZIhvcNAQEL
            BQADggEBAEBeBJxb/yBmsu7WAQUJ7FHJcVGqa6guyK1TjQjaGUWj51qu4tj3vcQv
            VsJCNB/FNrn25WLs5mKPMUe0LTimxomd6fHjP78PbLD1PM34taqdONlJjMJ9h0Ac
            UE9Rmd+T7qCBKXZ93kCL64NMJAMZUGv4Tmu6K/Oc1M8NlCoj+XyZD//85VLjJCTl
            NT+h5tcFkhYQKhIQdUoXWNsSOrjjy6kL+1XyhR3X7xpU4qfV3vqKfgZrQeGXH7Ba
            pnwXU4Fb+aAx6AUNje26r9fxGCPEy75tTQVPZwtFF+XbY95CDF/ExeB8Rbyuw9UR
            SRNUK8EjiNlhKUGCGG38wK7+h/nIeYw=
            -----END CERTIFICATE-----
    
        - name: fake_cert02.crt
          pem: |
            -----BEGIN CERTIFICATE-----
            MIIEAzCCAuugAwIBAgIJAK6b4p4LbqpLMA0GCSqGSIb3DQEBCwUAMIGXMQswCQYD
            VQQGEwJVUzELMAkGA1UECAwCTkUxEDAOBgNVBAcMB1JhbHN0b24xFTATBgNVBAoM
            DERpbm9oZWFkIExMQzEWMBQGA1UECwwNZmFrZSBBRiBjZXJ0czEXMBUGA1UEAwwO
            c2FsLmRvbWFpbi5jb20xITAfBgkqhkiG9w0BCQEWEmRlcmVrQGRpbm9oZWFkLmNv
            bTAeFw0xODA3MTcxODQ5MzVaFw0xOTA3MTcxODQ5MzVaMIGXMQswCQYDVQQGEwJV
            UzELMAkGA1UECAwCTkUxEDAOBgNVBAcMB1JhbHN0b24xFTATBgNVBAoMDERpbm9o
            ZWFkIExMQzEWMBQGA1UECwwNZmFrZSBBRiBjZXJ0czEXMBUGA1UEAwwOc2FsLmRv
            bWFpbi5jb20xITAfBgkqhkiG9w0BCQEWEmRlcmVrQGRpbm9oZWFkLmNvbTCCASIw
            DQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALvJOJRhGCenTaHCZvDZ14Rz6Qn9
            IU+SKRhE0PfcPhY936ZmzCDtfLM9zyq8/gEM95NRAb+vtgKGE2rUseiMVF54mIsB
            SY98eAlPK9o7C+kJRlJua11eU6Pcjf5rQoGO0EmbaiikyOemlCGS+J7rjAXg6wvD
            jQWRK/Rcvc62yVb55HV1ME3g2GrwhE+03BTtrqryFNif/6sOKVIPoKU26Imwz8Ob
            h1d13v7OrApoWUv2NiYGZCU664DaZsJDVbyy5pF39KgxNPtJGC7wnHielL1b/bc5
            MpDJ3DOSGgRFa4Rn9XceB1LvbWrwmmrtp9cRFIjQ//khSaFQP4Z4IIVuZbMCAwEA
            AaNQME4wHQYDVR0OBBYEFE5y+Z2XbLr/4zuPwd/brKa6tpfQMB8GA1UdIwQYMBaA
            FE5y+Z2XbLr/4zuPwd/brKa6tpfQMAwGA1UdEwQFMAMBAf8wDQYJKoZIhvcNAQEL
            BQADggEBAHW7eTVCVmrw1ntLBmVJJEwQ4QaQbdXWbaIdR6iFpnR87zXgFFlXLMSB
            0sfXTjXW2bIxeZjRgROUZAf++JTaaEfDwjQ9pT1bhb253quj6Zpepk6iA/iuzEyJ
            5/XOx3NFVhdb1ArRIvbvepOgksKnQiuCsyGvEuEvG9orQQI0MtHz+J1uElkOkIO7
            i+NmESg4R8b3mDmhUIlReK25dZ86zNaJbb0DbDiuCMdjVs5A3cLiCK57drRoDVT2
            hFPXYoK6ydBPD2pLYv0JlZyfN87BqfMLh6cPlkYuqOm7auetWyZ6d5Oa3DVjOCKV
            q2tMaYC69++8bOY1l9v5QewVRpnshXQ=
            -----END CERTIFICATE-----
```

```yaml
- name: ROLE | Add root certificate authorities 
  hosts: web
  roles:
     - role: ar_linux_root_ca
       linux_root_ca_filepath: /etc/ssl
```

## Author Information

|Author              |E-mail                   |
|:-------------------|:------------------------|
|Derek 'dRock' Halsey|derek.halsey@dinohead.com|

## License

MIT License

Copyright (c) 2019 Dinohead LLC

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Role Development Information

### Testing

### Git SCM
Please refer to the .gitignore file and update accordingly depending on your
development environment, etc.  The particular file was generated at 
[gitignore.io](https://www.gitignore.io/) and contains settings for the following:
  - Ansible
  - Python
  - Vim
  - Eclipse
  - IntelliJ IDEA
  - Linux
  - Windows
  
### Versioning
Please update [VERSION.md](./VERSION.md) as you release new versions of your role and try to
abide by [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

### Self-contained
Please try to keep this role as self-contained as possible such that it may be
simply installed (e.g. `ansible-galaxy install`) and applied as part of a 
playbook.
