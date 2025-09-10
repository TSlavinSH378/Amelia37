Amelia uses encryption throughout the software application. A boot secret is used to seed all encryption activities, including decrypt application properties used for encryption. Additionally, for questions that require user input of sensitive data, a BPN Ask task can be set up for “Secure user input.” Users responses will be replaced by dots and Amelia’s interactions also mask their response.
All communication between Amelia components including RabbitMQ and Redis use TLS 1.2 encrypted communication channels. Amelia and user utterances are sent encrypted to the database.
# Amelia Boot Secret
At installation time a secret must be chosen.  This secret should be at least 16 characters long and entirely random.  All encryption operations in Amelia cascade off this secret.  It is used to decrypt application properties used to unlock various encryption keys stored in the Amelia keystore.
At application startup time, this secret must be available as an environment variable. Other mechanisms or key management systems may be used to inject this environment variable based on the installation environment.
> [!info]  
>
> **If the boot secret is lost, it will not be possible to recover encrypted data.**

# Application Properties
Any application properties can be encrypted. All passwords at a minimum should be encrypted. Amelia utilizes [Jasypt](http://www.jasypt.org/) for encrypting properties along with its [Spring Boot Integration](https://github.com/ulisesbocchio/jasypt-spring-boot). These properties are encrypted with the boot secret described above.
A utility is included to encrypt and decrypt values from the command line.
For example, to encrypt the property "foo.password" with the value "as8cr8t" and the secret "panda" would generate ENC(Btc0J8D7CpH4RiqlZRRlr6RbT8xVXlW07AR9fvo92IM=) which is set in the properties file:
``` groovy
foo.password=ENC(Btc0J8D7CpH4RiqlZRRlr6RbT8xVXlW07AR9fvo92IM=)
```
# Amelia Keystore and Data Encryption
The Amelia keystore holds the encryption keys used to encrypt sensitive data stored throughout Amelia.  At installation time, a new keystore must be created. Generating a new keystore adds a single self-signed certificate. This certificate is used for the TLS listeners of amelia-web and amelia-engine. Set the ownership of the certificate file to the amelia user and permissions such that only the amelia user can read and write to it.
Next, the random store password is encrypted with the amelia boot secret and added to the amelia-web and amelia-engine's application.properties files. The amelia-engine and amelia-web services are started with the encryption data. In a clustered environment, the keystore needs to be copied to each node in the cluster. At startup time, amelia-engine generates 256bit AES keys and adds them to the configured keystore.
> [!info]  
>
> **If the keystore file is lost, it is not possible to recover encrypted data.**
