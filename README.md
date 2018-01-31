# certificates
Zertifikate – Die verschiedenen Formate
___
**PEM**  (Privacy Enhanced Mail)
    
Das PEM-Format wird auch häufig von Zertifizierungsstellen verwendet. Es ist Base64 kodiert und kann neben dem reinen Zertifikat auch Intermediate-Zertifikate, Root-CAs und private Schlüssel beinhalten.

Die Dateierweiterung ***.pem*** kommt meist zum Einsatz, wenn Zertifikate und der Privatschlüssel in einer Datei gespeichert werden. 
___
**CERT, CER oder CRT**

.cert, .cer und .crt sind Dateien im PEM-Format, welche eine andere Dateiendung besitzen. Diese Endungen kommen zum Einsatz, wenn zur Installation einzelne Dateien für die Zertifikate verlangt werden.
___
**KEY**

Die .key-Datei liegt im PEM-Format vor und beinhaltet den privaten Schlüssel eines Zertifikats. 
Sie kann von Hand aus einer PEM Datei erzeugt werden. 

___
**DER** (Distinguished Encoding Rules)

Die DER(.der)-Datei ist das binäre Form der Base64-kodierten PEM(.pem)-Datei. Neben Windows kommen Zertifikate im DER(.der)-Format auch unter Java zum Einsatz. Eine DER Datei kann im Gegensatz zu einer PEM Datei, die mehrere Zertifikate enthalten kann, nur für ein einziges Zertifikat verwendet werden.

Private Schlüssel oder der Zertifizierungspfad können mit diesem Format nicht gespeichert werden.

___
**PFX oder P12**

PFX(.pfx) und P12(.p12) sind binäre Format die neben dem Zertifikat auch alle Zertifikate des Zertifizierungspfads und den privaten Schlüssel enthalten. 

Alles in einer Datei. Es möglich die  Datei passwortgeschützt zu speichern. Dieses Format wird oft zum Import und Export von Zertifikaten und privaten Schlüsseln unter Windows und Java verwendet.

___
**P7B oder P7C**
P7B(.p7b) und P7C(.p7c) werden in der Regel mit Base64 kodiert und können neben einem Zertifikat auch alle Zertifikate des Zertifizierungspfads enthalten. 

Im Gegensatz zu PEM existiert eine Definition, wie die Zertifikate des Zertifizierungspfads eingebunden werden müssen. 

Private Schlüssel sind nicht möglich. .p7b- und .p7c-Dateien sind unter Windows und in Apache Tomcat üblich.

___
**CSR** (Certificate Signing Request)

Ein Certificate Signing Request (CSR, deutsch Zertifikatsignierungsanforderung) ist ein standardisiertes Format zum Anfordern eines digitalen Zertifikats. 

Der CSR enthält den öffentlichen Schlüssel und weiteren Angaben über den Antragsteller des Zertifikats. 

Die Zertifizierungsanfrage kann von einer Zertifizierungsstelle (CA) signiert werden und man erhält ein digitales Zertifikat zurück.

___
**CRL** (Certificate Revocation List)

Mit Hilfe einer CRL (Zertifikatsperrliste) können Zertifikate vor dem Ende des eigentlichen Ablaufdatums gesperrt werden. 

In der Regel ist dies der Fall, wenn der private Schlüssel nicht mehr sicher oder der Zertifikatsinhalt falsch ist.

**Formate konvertieren**

**PEM zu DER**
```cmd
openssl x509 -outform der -in certificate.pem -out certificate.der
```

**PEM zu P7B**
```cmd
openssl crl2pkcs7 -nocrl -certfile certificate.cer -out certificate.p7b -certfile CACert.cer
````

**PEM zu PFX**

```cmd
openssl pkcs12 -export -in certificate.crt -inkey privateKey.key -out certificate.pfx -certfile CACert.crt
````

**PFX zu PEM**

```cmd
openssl pkcs12 -in certificate.pfx -out certificate.pem -nodes
````

**DER zu PEM**

```cmd
openssl x509 -inform der -in certificate.cer -out certificate.pem
````

**P7B zu PEM**

```cmd
openssl pkcs7 -print_certs -in certificate.p7b -out certificate.pem
```

**P7B zu PFX**

```cmd
openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer 

openssl pkcs12 -export -in certificate.cer -inkey privateKey.key -out certificate.pfx -certfile CACert.cer
````

**CSR erstellen**

```cmd
openssl req -new -nodes -keyout host.domain.tld.key -out host.domain.tld.csr
```

**Self-Signed**

```cmd
openssl req -x509 -days 1826 -new -nodes -keyout host.domain.tld.key -out host.domain.tld.crt -newkey rsa:4096 -sha256
```