#HS Canonical

##Introduction
###Note: This Documentation Is Currently Being Updated For This Environment
HotSchedules provides a Web Services API for client integration. This API can be used to exchange Employee, Labor and Sales information with HotSchedules directly, rather than via file exchange or HSConnect integration. 

This API consists of a set of SOAP web services, implemented using the CXF framework. Calls to these services should be done via serialized data objects. Services will use a UsernameToken security header, which must be explicitly added by the third party before we will accept their web service calls. We will provide each company with a username and password for secure access to the API services.

##Requesting a username/password
Please contact your HotSchedules account manager for a username/password.

##Required SSL certificates
Our web services connect through an SSL encrypted connection, requiring a certificate to be present on the client side. HotSchedules uses DigiCert for our services.hotschedules.com SSL certificate. Because GoDaddy will not generate SSL certificates directly off of the root cert, we also require their intermediate certificate to be installed on the client. The certificates required can be downloaded directly from GoDaddy.

[Download Location: https://certs.godaddy.com/anonymous/repository.seam] (https://certs.godaddy.com/anonymous/repository.seam)

The two certificates required are,

**Go Daddy Class 2 Certification Authority Root Certificate**<br>
gd•class2•root.crt
<br>
Certificate File Hash (sha1) : F0 EC B0 51 00 08 A3 1A D3 60 9A C8 C5 54 10 C3 9B F4 BA A2
<br>
Certificate Thumbprint (sha1) : 27 96 ba e6 3f 18 01 e2 77 26 1b a0 d7 77 70 02 8f 20 ee e4

**Go Daddy Secure Server Certificate (Intermediate Certificate)**
<br>
gd_intermediate.crt
<br>
Certificate File Hash (sha1) : 17 93 21 10 65 FA 24 D9 46 53 18 83 DE 62 CA 0F AE 4D 61 7D
<br>
Certificate Thumbprint (sha1) : 7C 46 56 C3 06 1F 7F 4C 0D 67 B3 19 A8 55 F6 0E BC 11 FC 44
<br>

Once you have the certificates downloaded, you must install them in your keystore. Here is an Oracle article explaining keystores as well as how to install a certificate into your keystore:

[Oracle Certificate Installation HOW•TO] (http://www.google.com/url?q=http%3A%2F%2Fdocs.oracle.com%2Fjavase%2F7%2Fdocs%2Ftechnotes%2Ftools%2Fwindows%2Fkeytool.html&sa=D&sntz=1&usg=AFQjCNFqKb0kHsXRHyMsnV_orWc2nh1uvA)
<br>
Generally, the keystore file is created in your installed JRE's directory (/jre/lib/security). The default name is cacerts, and the default password is changeit. If you need to generate a new keystore file, see the following link for directions.

[Apache SSL Configuration HOW•TO](http://www.google.com/url?q=http%3A%2F%2Ftomcat.apache.org%2Ftomcat-4.1-doc%2Fssl-howto.html&sa=D&sntz=1&usg=AFQjCNGsATO2CXnXxtArzvoeu8JTVZFQ6g)
<br>
Once the keystore is located in the /lib/security directory of your Java install, and the certificates are installed in the keystore, your code should be able to correctly navigate the SSL connection.