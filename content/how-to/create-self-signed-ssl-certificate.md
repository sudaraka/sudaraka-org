{
  "title": "Create self-signed SSL certificate",
  "description": "Create self-signed SSL certificate - step by step explanation of creating self-signed ssl certificate for apache web server with openssl.",
  "keywords": "self-signed ssl certificate, openssl, apache",
  "date": "2012-08-12"
}

Authentication part of the SSL communication works on a private-public key
based trust system. In other words you have a key that is signed by another
key from a 3rd party which rest of the world (or the people who needs to
verify you) trust. This signed key is called a certificate.<!--more-->

It is however possible for you to sign your own certificate, but this
certificate wont be trusted by others but it will provide the SSL encryption
just like a paid SSL certificate.

Few scenarios why you would need/use such certificate are:

  - Provide encrypted communication between two parties that are already trust each other (i.e. Web application on a intranet)
  - Development or demo web site that needs to simulate the production environment with SSL

&nbsp;

## Private Key

First step in the process is to generate a private key, which will be your
unique signature to sign certificates.

<pre class="console">
<strong>$</strong> <kbd>openssl genrsa -aes256 -out server.key 4096</kbd>
Generating RSA private key, 4096 bit long modulus
..............++
..........................................................................................................
.......................................................++
e is 65537 (0x10001)
Enter pass phrase for server.key:
Verifying - Enter pass phrase for server.key:
</pre>

&nbsp;

We have created a 4096-bit long key with AES256 encryption and it has asked
us for a password to protect the key with. Generated key will be saved to the
file named server.key, You need to keep this key in a safe place as it will
be needed in the future to extend the validity of the SSL certificate.

Also if someone get hold of this key, they will be able to generate duplicate
certificates for your server.

&nbsp;

## Certificate Sign Request

Next step is to generate a Certificate Signing Request (CSR). CSR contains a
signature of your server along with some data that are displayed to the
public when some one look at this certificate (i.e Company name, address,
etc.)

<pre class="console">
<strong>$</strong> <kbd>openssl req -new -key server.key -out demo.csr</kbd>
Enter pass phrase for server.key:
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:LK
State or Province Name (full name) [Some-State]:
Locality Name (eg, city) []:Pannipitiya
Organization Name (eg, company) [Internet Widgits Pty Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:sudaraka.org
Email Address []:info@sudaraka.org

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
</pre>

&nbsp;

You will first need to enter the password for your key file which you created
in the earlier step. Every thing after that are optional details except for
the "Common Name" which is the exact domain name you are creating this
certificate for. * character can be used as a wild-card.

In a normal procedure where you get your SSL certificate signed by a 3rd
party authority, you will be sending this CSR to the relevant authority to be
signed. This is where the self-sign process forks away from that procedure.

&nbsp;

## Certificate Signing

You can use the same key we created above to sign the CSR, or you can create
a new key by following the same instructions. Let's assume you created a
second key called sign.key.

<pre class="console">
<strong>$</strong> <kbd>openssl x509 -req -days 365 -in demo.csr -signkey sign.key -out demo.crt</kbd>
Signature ok
subject=/C=LK/ST=Some-State/L=Pannipitiya/O=Internet Widgits Pty Ltd/CN=sudaraka.org/emailAddress=info@sudaraka.org
Getting Private key
Enter pass phrase for sign.key:
</pre>

&nbsp;

You now have everything that is needed to add the SSL certificate to Apache
web server (demo.crt and sever.key)

&nbsp;

## Usage

In the Apache configuration files locate the virtual host you want to add
this SSL certificate and add the following.

```
SSLEngine on
SSLCertificateFile "/path/to/demo.crt"
SSLCertificateKeyFile "/path/to/sign.key"
```

&nbsp;

One possible issue here is since our sign.key is password protected, Apache
will require that password every time it starts and it has to be entered
interactively. This is not possible because in most systems Apache run as a
daemon process. Solution is to remove the password from the sign.key that we
use for Apache like below.

<pre class="console">
<strong>$</strong> <kbd>openssl rsa -in sign.key -out sign.key</kbd>
Enter pass phrase for sign.key:
writing RSA key
</pre>

&nbsp;

Now restart Apache and you should be good to go.
