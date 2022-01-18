## [Build an HTTPS Service](https://docs.mulesoft.com/mule-runtime/4.4/build-an-https-service)

> Generate a keystore.jks

- creates a keystore.jks file with hostname SAN=DNS:localhost,IP:127.0.0.1 
```
keytool -help
```
```
keytool -genkeypair -keystore keystore-dev.jks   -dname "CN=localhost, OU=ForTraining, O=dKitaw, L=Unknown, ST=Unknown, C=USA"  -keypass myStrongPassword  -storepass myStrongPassword  -keyalg RSA   -keysize 2048  -alias mule_server  -ext SAN=DNS:localhost,IP:127.0.0.1 -validity 365
```

> Add the generated keystore.jks file to your Anypoint Studio Mule app folder in src/main/resources.

> Configure the HTTP Listener
```xml
<http:listener-config name="HTTP_Listener_config" doc:name="HTTP Listener config" doc:id="9f3f085d-a5ea-4769-9997-c4f882b176d8" >
    <http:listener-connection host="0.0.0.0" port="${https.port}" protocol="HTTPS">
        <tls:context >
            <tls:key-store keyPassword="myStrongPassword" password="myStrongPassword"  path="keystore-dev.jks" alias="mule_server"/>
        </tls:context>
    </http:listener-connection>
</http:listener-config>
<configuration-properties doc:name="Configuration properties" doc:id="51197ad9-2a4e-478e-8bec-904f691d9911" file="dev.yaml" />
```

> set https in configuration
- dev.yaml
```yaml
http:
  port: "8081"
https:
  port: "8081"
```