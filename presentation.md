autoscale: true

# [fit] Let's Encrypt

# [fit] All the Things

![](media/ben-garratt-134770.jpg)

---

![autoplay mute](media/lets-encrypt-example.mov)

^ Let's Encrypt is a certificate authority that provides TLS/SSL certificates.

^ So you can get a nice green pad lock on your website free of change without any human interaction.

^ This presentation will be covering HTTP over SSL, though Let's Encrypt allows for certificates using any protocol.

---

# What is
# [fit] HTTPS?

^ So what makes HTTPS so special.

---

# [fit] HTTP
# [fit] `+`
# [fit] Security

^ It's the normal everyday HTTP protocol with an added layer of security.

---

![left](media/http-mylesb-ca.png)

![right](media/https-mylesb-ca.png)

^ This added layer of security make sure that your traffic is between you and the server.

^ So passwords, communications, banking information, detailed plans to overthrow an orange hair president, or anything else you want private can't be intercepted by a third party.

---

![](media/00-Start.png)

# [fit] A quick explanation on how

# [fit] HTTPS Works

---

![](media/01-ClientHello.png)

^ The client computer sends a `ClientHello` message to the server with its TLS version, list of cipher algorithms, and compression methods available.

---

![](media/02-ServerHello.png)

^ The server replies with a `ServerHello` message to the client with the TLS version, selected cipher, selected compression methods and the server's public certificate signed by a CA.

^ The certificate contains a public key that will be used by the client to encrypt the rest of the handshake until a symmetric key can be agreed upon.

---

![](media/03-CA_Verify.png)

^ The client verifies the server digital certificate against its list of trusted CAs.

---

![](media/04-Random_Bytes.png)

^ If trust can be established based on the CA, the client generates a string of pseudo-random bytes and encrypts this with the server's public key.

^ These random bytes can be used to determine the symmetric key.

---

![](media/05-Server_Decrypts.png)

^ The server decrypts the random bytes using its private key and uses these bytes to generate its own copy of the symmetric master key.

---

![](media/06-Client_Finished.png)

^ The client sends a `Finished` message to the server, encrypting a hash of the transmission up to this point with the symmetric key.

---

![](media/07-Server_Finished.png)

^ The server generates its own hash, and then decrypts the client-sent hash to verify that it matches.

^ If it does, it sends its own Finished message to the client, also encrypted with the symmetric key.

---

![](media/igor-ovsyannykov-165874.jpg)

^ From now on the TLS session transmits the application data encrypted with the agreed symmetric key.

---

![](media/rob-heaton.jpg)

> Whilst the little green padlock and the letters "https" in your address bar don’t mean that there isn’t still ample rope for both you and the website you are viewing to hang yourselves elsewhere, they do at least help you communicate securely whilst you do so.
-- Rob Heaton, [How does HTTPS actually work?](http://robertheaton.com/2014/03/27/how-does-https-actually-work/), 27 March 2017

^ HTTPS doesn't protect you from all threats, it at least make sure the communication between the client and server are secure.

---

# How does
# [fit] Let's Encrypt Work

^ So how does Let's Encrypt work?

---

# Three Components

*   Server → **Boulder**
*   Client → **Let's Encrypt**
    *   Plugins for the different web servers
*   Protocol → **ACME**

^ There are three components to Let's Encrypt.

---

# Boulder

*   Written in Go
*   Responsible for handling all the CA procedures
    *   **Issuing**,
    *   **Renewal**,
    *   and **Revocation**.
*   Open Source: <https://github.com/letsencrypt/boulder>

^ Boulder the server is written in Go, and is responsible for handling all the CA procedures of issuing, renewal, and revocation of the certificates.

^ It's basically a HTTPS RESTful API interface.

---

# letsencrypt

*   Written in Python
*   Responsible for the interacting with the remote server
*   Open Source: <https://github.com/letsencrypt/letsencrypt>

^ letsencrypt is the client written in Python, and is responsible for landing the interaction with the remote server and handles your certificates.

---

## letsencrypt Plugins

*   The client comes with plugins to **simply** and **automate** the authentication and creation of certificates.

^ letsencrypt comes with plugins for popular web servers such as Apache and Nginx.

---

# ACME

*   Stand for Automated Certificate Management Environment
*   Exchanges of **JWS** between the client and server.

^ It's based on exchanges of signed JSON files, also known as JSON Web Signature.

^ These documents contains all the requests and the responses between the client and server.

---

# ACME does Three Things

1.  **Proves** that the client is the owner of the domain.
2.  **Obtain** a new certificate for the domain.
3.  **Revoke** or **Renew** a certificate for the domain.

^ The ACME protocol does three things.

^ It proves that the client is the owner of the domain.

^ It obtains the new certificate for the domain.

^ It also revoke or renews a certificate for the domain.

---

![](media/youtube-thumbnail.jpg)

# [fit] More Detailed Information about
# [fit] How Let's Encrypt Works

* Watch this video by Josh Aas: <https://youtu.be/ksqTu7TX83g>

^ If you want more information about the Let's Encrypt protocol. Watch this hour long video by Josh Aas.

---

# [fit] Drawbacks

^ There are a few drawbacks to using a Let's Encrypt certification.

---

![](media/olu-eletu-38649.jpg)

# No Organization or Extended Validation Certificates

^ You can't have an Organization Validation or Extended Validation certificates.

---

![](media/stephanie-krist-100516.jpg)

# No wildcards

^ Wildcard domains aren't support, this is the asterisk.

^ This might be a feature in the future. But I hope it's not.

---

![](media/stefan-stefancik-105372.jpg)

# Only HTTP domain verification

^ The only way to verify that you own a domain name is though HTTP.

^ DNS verification will be provided in the future.

---

![](media/give-me.gif)

# [fit] How do you get a
# [fit] Certificate

---

# [fit] Visit <https://certbot.eff.org/>

![](media/certbot-eff-org.png)

^ Go to certbot.eff.org.

---

![](media/certbot-eff-org.png)

^ Select what web server and operating system you are using.

---

![fit](media/certbot-eff-org-installation-instructions.png)

^ The follow the installation instructions.

---

# [fit] Questions?

---

# References

*   <https://github.com/alex/what-happens-when#tls-handshake>
*   <https://www.slideshare.net/NancyThanki/lets-encrypt-wait-why-how-wc-pune>
*   <https://www.slideshare.net/cortinico/lets-encrypt-free-certificates-for-everyone>

# Images

*   <https://unsplash.com/collections/594884/lets-encrypt-presentation>
