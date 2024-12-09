# Certificate Overview

This repository provides a comprehensive overview of digital certificates, including types, validation methods, use cases, and the role of Certificate Authorities (CAs) in digital security. The purpose is to create a reference for developers, system administrators, and anyone interested in understanding certificates, their importance, and their applications.

---

## Introduction

Digital certificates are essential for secure communications over the internet, offering 
- **encryption, **
- **authentication, **
- **and data integrity.** 
They are widely used to secure websites, sign software, verify email authenticity, and more. This repository serves as an educational resource for anyone seeking to understand certificates and how they contribute to online security.

## Certificate Types

### Validation Levels

Certificates are classified based on the validation level provided by the Certificate Authority (CA):

- **Domain Validation (DV)**: Basic validation to ensure domain ownership, typically involving DNS or email verification. Suitable for personal websites or internal testing.
- **Organization Validation (OV)**: Requires the CA to verify the organization's identity, adding credibility. Commonly used by businesses to establish trust with their users.
- **Extended Validation (EV)**: The highest level of validation, with extensive background checks on the organization. EV certificates often display the organization’s name in the browser’s address bar, enhancing user trust.

### Usage and Scope

Certificates can also differ based on their scope and usage:

- **Single-Domain Certificates**: Secure a single domain, such as `example.com`.
- **Wildcard Certificates**: Secure a domain and all of its subdomains at one level (e.g., `*.example.com`).
- **Multi-Domain Certificates (SAN/UCC)**: Secure multiple domains and/or subdomains in one certificate, ideal for complex setups with multiple services (e.g., `example.com`, `example.net`, `sub.example.com`).

### Specialized Certificates

There are also specialized certificates tailored to specific use cases:

- **Code-Signing Certificates**: Verify the integrity and origin of software, preventing tampering or unauthorized alterations.
- **E-Mail Certificates (S/MIME)**: Enable email encryption and authentication, ensuring the security and authenticity of email communications.
- **Client Certificates**: Authenticate users or devices, often used in corporate environments to secure access to sensitive systems.
- **Root and Intermediate Certificates**: Foundational certificates used by CAs to build trust chains, validating other issued certificates.
- 
## Public Key Infrastructure (PKI)
![PKI](PKI.drawio.svg)

### Registration Authority (RA)

The **Registration Authority (RA)** is an essential component in the Public Key Infrastructure (PKI), serving as an intermediary between the Certificate Authority (CA) and certificate applicants. Its primary purpose is to handle identity verification and validation for certificate requests before they are issued by the CA.

#### Key Purposes of the RA

1. **Identity Verification**
   - The RA is responsible for verifying the identity of individuals, organizations, or devices requesting a certificate. This process includes checking documentation, conducting background checks, and ensuring the applicant has legitimate control over the requested domain or organization name.

2. **Authorization of Requests**
   - After completing identity verification, the RA authorizes the request, confirming that the applicant is eligible for the certificate. This process helps ensure that only verified, trustworthy applicants receive certificates, reducing the risk of fraud.

3. **Support for CA Workload**
   - By handling validation processes, the RA reduces the workload on the CA. This division of responsibilities allows the CA to focus on issuing and managing certificates efficiently, without compromising on security standards.

4. **Enhanced Security**
   - With the RA taking on the responsibility of verifying identities and documentation, the PKI system becomes more secure. The RA minimizes the chances of unverified or fraudulent certificates being issued, which is crucial for maintaining trust in the PKI.

5. **Local Verification in Distributed Environments**
   - For large organizations or geographically distributed systems, RAs are often deployed locally to expedite the verification process. This allows for quicker issuance of certificates by handling validations closer to the applicant's location, making the process more efficient.

### Certificate Authority (CA)

A **Certificate Authority (CA)** is the core component of the Public Key Infrastructure (PKI), responsible for issuing, managing, and revoking digital certificates. The CA plays a critical role in establishing and maintaining trust in secure online communications by verifying and certifying the identity of entities (such as individuals, organizations, or devices). 

#### Key Purposes of the CA

1. **Issuing Certificates**
   - The primary function of a CA is to issue digital certificates after verifying the identity of the applicant. These certificates are used to authenticate and secure communications, such as HTTPS for websites, secure email, and signed software. The issuance process involves digitally signing the certificate, which confirms that the CA vouches for the identity and public key of the certificate holder.

2. **Building Trust through the Trust Chain**
   - The CA establishes a **Trust Chain** in the PKI. This chain typically starts with a **Root Certificate**, which is self-signed and trusted by default in operating systems and browsers. The Root Certificate signs **Intermediate Certificates**, which, in turn, sign **End-Entity Certificates** (e.g., for websites). This chain ensures that a user can trust the end certificate based on the established trust in the CA.

3. **Managing and Renewing Certificates**
   - CAs are responsible for the lifecycle management of certificates, including renewal notifications, re-issuance, and updates. This process ensures that certificates remain valid and secure over time, minimizing risks associated with expired or outdated certificates.

4. **Revoking Certificates**
   - CAs can revoke certificates if they are compromised, misused, or no longer needed. They maintain **Certificate Revocation Lists (CRLs)** and offer **Online Certificate Status Protocol (OCSP)** services, allowing clients and browsers to check the status of certificates. Revocation helps protect users by preventing access to compromised entities.

5. **Enhancing Security and Trust**
   - The CA is a trusted entity responsible for ensuring that only verified applicants receive certificates. By maintaining strict validation processes, the CA helps prevent the issuance of certificates to fraudulent or malicious entities, thus preserving trust across the internet.

### Validation Authority (VA)

A **Validation Authority (VA)** is a component within the Public Key Infrastructure (PKI) responsible for validating the status and authenticity of digital certificates. The VA works in conjunction with the Certificate Authority (CA) to provide real-time information on the validity of certificates, ensuring that entities relying on certificates can trust them to be secure and unrevoked.

#### Key Purposes of the VA

1. **Real-Time Certificate Validation**
   - The primary role of a VA is to validate whether a certificate is still valid and trustworthy. This validation includes checking if a certificate has been revoked, expired, or otherwise compromised. The VA ensures that end-users, systems, and applications receive up-to-date certificate status information in real time.

2. **Support for Revocation Checking**
   - VAs work with the CA’s revocation mechanisms to confirm the current status of certificates. They offer **Online Certificate Status Protocol (OCSP)** responses or maintain **Certificate Revocation Lists (CRLs)**. By querying a VA, clients can confirm that a certificate is valid and has not been revoked, preventing users from accessing fraudulent or compromised services.

3. **Enhanced Security for High-Security Environments**
   - In sensitive environments such as financial institutions, healthcare, or government sectors, real-time validation is critical. A VA provides an extra layer of security by quickly identifying and blocking certificates that are no longer valid, which helps prevent potential fraud, unauthorized access, or data breaches.

4. **Load Reduction for the CA**
   - By offloading certificate validation tasks to the VA, the CA can focus on issuing and managing certificates rather than responding to continuous validation requests. This separation of responsibilities enhances the efficiency of the PKI system and ensures faster, more reliable validation responses for end-users.

5. **Trust Chain Reinforcement**
   - The VA plays a crucial role in reinforcing the PKI trust chain by constantly monitoring and verifying the status of certificates. When a client checks with a VA, they receive confirmation that the certificate is still backed by the trust chain, supporting integrity and trust in secure communications.

### Certificate Requestor

The **Certificate Requestor (RA)** is an essential participant in the Public Key Infrastructure (PKI) responsible for initiating the process to obtain a digital certificate. The Requestor could be an individual, organization, server, or device seeking to secure communications, authenticate identity, or ensure data integrity through the use of a digital certificate.

#### Key Responsibilities of the Certificate Requestor

1. **Generating a Certificate Signing Request (CSR)**
   - The Certificate Requestor begins by creating a **Certificate Signing Request (CSR)**. This request includes the Requestor's public key and information that will identify them in the certificate (such as domain name, organization details, and contact information). The CSR is then sent to a Certificate Authority (CA) for validation.

2. **Providing Accurate Information for Verification**
   - The Requestor must ensure that all information in the CSR is accurate and up-to-date. This information will be verified by the CA or a Registration Authority (RA) to confirm the Requestor’s identity and ownership over the domain or organization name in question.

3. **Completing Identity Validation Steps**
   - Depending on the type of certificate (e.g., Domain Validation, Organization Validation, Extended Validation), the Requestor may need to complete additional validation steps, such as DNS verification, email confirmation, or providing legal documentation to verify organizational details.

4. **Managing Private Key Security**
   - The Requestor is responsible for securely generating and storing their private key, which pairs with the public key in the CSR. This private key should never be shared with anyone, including the CA, as it is critical for the security of the Requestor’s digital identity.

5. **Implementing and Maintaining the Certificate**
   - Once the certificate is issued, the Requestor must install it on the appropriate server or device and configure it correctly to enable secure communications. The Requestor is also responsible for renewing or reissuing the certificate before it expires to maintain continuous security.

6. **Revoking the Certificate if Necessary**
   - If the private key associated with the certificate is compromised or the certificate is no longer needed, the Requestor is responsible for notifying the CA to revoke the certificate. This action helps prevent misuse and maintains the security of the PKI system.


### Relying Party

The **Relying Party (RP)** is an essential participant in the Public Key Infrastructure (PKI), responsible for trusting and acting upon the validity of a digital certificate. Typically, the Relying Party is an entity (such as a user, application, server, or device) that relies on the certificate to authenticate identities, verify data integrity, and establish secure communication channels.

#### Key Responsibilities of the Relying Party

1. **Validating the Certificate's Authenticity**
   - The Relying Party must validate the certificate presented by another entity (e.g., a website, server, or individual). This validation includes checking the certificate's digital signature, issuer, expiration date, and chain of trust to confirm it was issued by a trusted Certificate Authority (CA).

2. **Checking Certificate Revocation Status**
   - The Relying Party needs to ensure that the certificate is still valid by checking its revocation status. This can be done using **Online Certificate Status Protocol (OCSP)** or **Certificate Revocation Lists (CRLs)**, which indicate if the certificate has been revoked by the CA due to compromise or other security issues.

3. **Establishing Secure Communication**
   - Once the certificate is validated, the Relying Party can establish an encrypted and authenticated connection with the certificate holder. This is common in HTTPS connections, email encryption, and other secure communications, ensuring data confidentiality and integrity.

4. **Trusting the Identity of the Certificate Holder**
   - By relying on the certificate, the Relying Party trusts that the entity presenting the certificate is indeed who they claim to be. This identity verification enables secure transactions, data exchanges, and communications, critical for services like online banking, e-commerce, and enterprise applications.

5. **Adhering to Security Policies**
   - The Relying Party may follow internal security policies that specify acceptable certificate types, trusted CAs, and revocation checking procedures. Ensuring these policies are followed helps maintain a secure environment and minimizes risks associated with untrusted certificates.

6. **Responding to Security Alerts and Changes in Trust**
   - If a certificate fails validation (e.g., it’s expired, untrusted, or revoked), the Relying Party should deny access or terminate the connection to avoid potential security threats. This proactive response helps safeguard the Relying Party from compromised or malicious entities.


## How Certificates Work

### Structure of a digital certificate

| Field                     | Description                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------|
| Common Name               | The domain name for which the certificate is issued.                                           |
| Issued By                 | The organization (Certificate Authority) that issued the certificate.                          |
| Issuing Certificate       | The intermediate certificate used to sign this certificate.                                    |
| Serial Number             | A unique identifier assigned to the certificate by the Certificate Authority.                  |
| Valid From                | The start date and time when the certificate becomes valid.                                     |
| Valid To                  | The end date and time when the certificate expires.                                            |
| Key Usage                 | Specifies the purpose of the certificate's public key (e.g., digital signature, key encipherment). |
| Extended Key Usage        | Further specifies the certificate's usage, such as TLS server or client authentication.         |
| Basic Constraints         | Indicates whether the certificate can act as a CA (e.g., "CA:FALSE" means it cannot issue certificates). |
| Subject Key Identifier    | A unique identifier for the certificate's public key, helping to differentiate keys.           |
| Authority Key Identifier  | Identifies the public key associated with the certificate's issuing CA.                        |
| Authority Info Access     | Provides information about the CA, including an OCSP responder URL and a link to the CA's certificate. |
| Subject Alternative Names | Lists additional domain names or IP addresses covered by the certificate.                      |

#### Example
```
-----BEGIN CERTIFICATE-----
MIIHbjCCBlagAwIBAgIQB1vO8waJyK3fE+Ua9K/hhzANBgkqhkiG9w0BAQsFADBZ
MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMTMwMQYDVQQDEypE
aWdpQ2VydCBHbG9iYWwgRzIgVExTIFJTQSBTSEEyNTYgMjAyMCBDQTEwHhcNMjQw
MTMwMDAwMDAwWhcNMjUwMzAxMjM1OTU5WjCBljELMAkGA1UEBhMCVVMxEzARBgNV
BAgTCkNhbGlmb3JuaWExFDASBgNVBAcTC0xvcyBBbmdlbGVzMUIwQAYDVQQKDDlJ
bnRlcm5ldMKgQ29ycG9yYXRpb27CoGZvcsKgQXNzaWduZWTCoE5hbWVzwqBhbmTC
oE51bWJlcnMxGDAWBgNVBAMTD3d3dy5leGFtcGxlLm9yZzCCASIwDQYJKoZIhvcN
AQEBBQADggEPADCCAQoCggEBAIaFD7sO+cpf2fXgCjIsM9mqDgcpqC8IrXi9wga/
9y0rpqcnPVOmTMNLsid3INbBVEm4CNr5cKlh9rJJnWlX2vttJDRyLkfwBD+dsVvi
vGYxWTLmqX6/1LDUZPVrynv/cltemtg/1Aay88jcj2ZaRoRmqBgVeacIzgU8+zmJ
7236TnFSe7fkoKSclsBhPaQKcE3Djs1uszJs8sdECQTdoFX9I6UgeLKFXtg7rRf/
hcW5dI0zubhXbrW8aWXbCzySVZn0c7RkJMpnTCiZzNxnPXnHFpwr5quqqjVyN/aB
KkjoP04Zmr+eRqoyk/+lslq0sS8eaYSSHbC5ja/yMWyVhvMCAwEAAaOCA/IwggPu
MB8GA1UdIwQYMBaAFHSFgMBmx9833s+9KTeqAx2+7c0XMB0GA1UdDgQWBBRM/tAS
TS4hz2v68vK4TEkCHTGRijCBgQYDVR0RBHoweIIPd3d3LmV4YW1wbGUub3Jnggtl
eGFtcGxlLm5ldIILZXhhbXBsZS5lZHWCC2V4YW1wbGUuY29tggtleGFtcGxlLm9y
Z4IPd3d3LmV4YW1wbGUuY29tgg93d3cuZXhhbXBsZS5lZHWCD3d3dy5leGFtcGxl
Lm5ldDA+BgNVHSAENzA1MDMGBmeBDAECAjApMCcGCCsGAQUFBwIBFhtodHRwOi8v
d3d3LmRpZ2ljZXJ0LmNvbS9DUFMwDgYDVR0PAQH/BAQDAgWgMB0GA1UdJQQWMBQG
CCsGAQUFBwMBBggrBgEFBQcDAjCBnwYDVR0fBIGXMIGUMEigRqBEhkJodHRwOi8v
Y3JsMy5kaWdpY2VydC5jb20vRGlnaUNlcnRHbG9iYWxHMlRMU1JTQVNIQTI1NjIw
MjBDQTEtMS5jcmwwSKBGoESGQmh0dHA6Ly9jcmw0LmRpZ2ljZXJ0LmNvbS9EaWdp
Q2VydEdsb2JhbEcyVExTUlNBU0hBMjU2MjAyMENBMS0xLmNybDCBhwYIKwYBBQUH
AQEEezB5MCQGCCsGAQUFBzABhhhodHRwOi8vb2NzcC5kaWdpY2VydC5jb20wUQYI
KwYBBQUHMAKGRWh0dHA6Ly9jYWNlcnRzLmRpZ2ljZXJ0LmNvbS9EaWdpQ2VydEds
b2JhbEcyVExTUlNBU0hBMjU2MjAyMENBMS0xLmNydDAMBgNVHRMBAf8EAjAAMIIB
fQYKKwYBBAHWeQIEAgSCAW0EggFpAWcAdABOdaMnXJoQwzhbbNTfP1LrHfDgjhuN
acCx+mSxYpo53wAAAY1b0vxkAAAEAwBFMEMCH0BRCgxPbBBVxhcWZ26a8JCe83P1
JZ6wmv56GsVcyMACIDgpMbEo5HJITTRPnoyT4mG8cLrWjEvhchUdEcWUuk1TAHYA
fVkeEuF4KnscYWd8Xv340IdcFKBOlZ65Ay/ZDowuebgAAAGNW9L8MAAABAMARzBF
AiBdv5Z3pZFbfgoM3tGpCTM3ZxBMQsxBRSdTS6d8d2NAcwIhALLoCT9mTMN9OyFz
IBV5MkXVLyuTf2OAzAOa7d8x2H6XAHcA5tIxY0B3jMEQQQbXcbnOwdJA9paEhvu6
hzId/R43jlAAAAGNW9L8XwAABAMASDBGAiEA4Koh/VizdQU1tjZ2E2VGgWSXXkwn
QmiYhmAeKcVLHeACIQD7JIGFsdGol7kss2pe4lYrCgPVc+iGZkuqnj26hqhr0TAN
BgkqhkiG9w0BAQsFAAOCAQEABOFuAj4N4yNG9OOWNQWTNSICC4Rd4nOG1HRP/Bsn
rz7KrcPORtb6D+Jx+Q0amhO31QhIvVBYs14gY4Ypyj7MzHgm4VmPXcqLvEkxb2G9
Qv9hYuEiNSQmm1fr5QAN/0AzbEbCM3cImLJ69kP5bUjfv/76KB57is8tYf9sh5ik
LGKauxCM/zRIcGa3bXLDafk5S2g5Vr2hs230d/NGW1wZrE+zdGuMxfGJzJP+DAFv
iBfcQnFg4+1zMEKcqS87oniOyG+60RMM0MdejBD7AS43m9us96Gsun/4kufLQUTI
FfnzxLutUV++3seshgefQOy5C/ayi8y1VTNmujPCxPCi6Q==
-----END CERTIFICATE-----
````
Decoded:

| Field                     | Value                                                                                  |
|---------------------------|----------------------------------------------------------------------------------------------|
| Common Name                 | www.example.org|
| Issued By                   | DigiCert Inc |
| Issuing Certificate         | DigiCert Global G2 TLS RSA SHA256 2020 CA1|
| Serial Number               |075BCEF30689C8ADDF13E51AF4AFE187|
| Valid From                  | 00:00:00 30 Jan 2024|
| Valid To                    | 23:59:59 01 Mar 2025 |
| Key Usage                   | Digital Signature, Key Encipherment|
| Extended Key Usage          | TLS Web Server Authentication, TLS Web Client Authentication|
| Basic Constraints           |CA:FALSE|
|Subject Key Identifier       | 4C:FE:D0:12:4D:2E:21:CF:6B:FA:F2:F2:B8:4C:49:02:1D:31:91:8A|
|Authority Key Identifier     |74:85:80:C0:66:C7:DF:37:DE:CF:BD:29:37:AA:03:1D:BE:ED:CD:17|
|Authority Info Access        |OCSP - URI:http://ocsp.digicert.com CA Issuers - URI:http://cacerts.digicert.com/DigiCertGlobalG2TLSRSASHA2562020CA1-1.crt|
|Subject Alternative Names    |DNS:www.example.org, DNS:example.net, DNS:example.edu, DNS:example.com, DNS:example.org, DNS:www.example.com, DNS:www.example.edu, DNS:www.example.net|

### TLS/HTTPS

TLS (Transport Layer Security) is the protocol that underpins HTTPS, providing secure communication over a network. A server certificate is a critical component in this process, enabling encrypted communication and verifying the server’s identity. Here’s how it works step-by-step:

1. Client Initiates a Connection

	•	The client (e.g., a web browser) sends a request to the server to establish a secure connection. This request is known as a “ClientHello.”
	•	The ClientHello includes information about supported cryptographic algorithms (ciphers), the TLS version, and other settings.

2. Server Responds

	•	The server responds with a “ServerHello,” selecting the cryptographic algorithms to use.
	•	The server also sends its digital certificate as part of the response.

3. Server Certificate

	•	The server certificate is issued by a trusted Certificate Authority (CA) and contains:
	•	The server’s domain name.
	•	The server’s public key.
	•	The CA’s digital signature.
	•	Expiry and validity information.
	•	The client validates the certificate:
	•	Verifies the CA’s signature to ensure the certificate has not been tampered with.
	•	Checks that the certificate is issued for the requested domain.
	•	Ensures the certificate is still valid (not expired or revoked).

4. Key Exchange

	•	The client and server perform a key exchange to establish a shared secret for encryption. Depending on the chosen method, this can involve:
	•	RSA: The client uses the server’s public key to encrypt a randomly generated pre-master secret, which only the server can decrypt with its private key.
	•	Elliptic Curve Diffie-Hellman (ECDH) or Diffie-Hellman (DH): Both parties contribute to generating a shared secret without directly transmitting it.

5. Session Key Generation

	•	Using the shared secret, the client and server independently compute the same session keys. These keys are symmetric and are used for encrypting communication during the session.

6. Secure Communication

	•	Both parties now use the session keys to encrypt and decrypt data, ensuring confidentiality and integrity.

7. Data Transmission

	•	All subsequent communication between the client and server is encrypted using the session keys.
	
	
	
![PKI](tls.png)

Key Benefits of Using a Server Certificate in TLS/HTTPS

	1.	Encryption: Prevents eavesdropping by encrypting data in transit.
	2.	Authentication: Verifies the server’s identity, ensuring users connect to the intended website.
	3.	Data Integrity: Detects tampering or corruption of data during transmission.

Role of Certificate Authority (CA)

A CA acts as a trusted third party, vouching for the authenticity of the server certificate. Clients trust CAs implicitly because their root certificates are pre-installed in browsers and operating systems.

This combination of encryption, authentication, and integrity is what makes HTTPS secure.

### mTLS

TLS (Transport Layer Security) and mTLS (Mutual TLS) are both protocols that provide secure communication over a network. While they share foundational mechanisms, they differ primarily in their purpose and how authentication is handled. 
Here’s a detailed comparison:
| Aspect                     | TLS                                                | mTLS                                               |
|----------------------------|----------------------------------------------------|---------------------------------------------------|
| Purpose                    | Ensures secure communication by encrypting data and authenticating the server to the client. | Provides secure communication with mutual authentication, verifying both the client and the server. |
| Authentication             | Only the server is authenticated using a certificate. | Both the server and the client are authenticated using certificates. |
| Client Certificate         | Not required; the client is not authenticated using a certificate. | Required; the client must present a valid certificate to authenticate itself. |
| Use Case                   | Commonly used in web browsing, where only the server needs to prove its identity. | Used in environments requiring high security, such as API communication, financial systems, or microservices. |
| Complexity                 | Easier to set up, as it requires only a server certificate. | More complex to configure, as both server and client certificates need to be managed. |
| Examples                   | HTTPS websites, web applications, email encryption. | Secure APIs, B2B integrations, internal microservices communication. |
| Trust Verification         | The client verifies the server's certificate against a trusted Certificate Authority (CA). | Both the client and server verify each other's certificates against trusted CAs. |
| Certificate Management     | Requires management of server certificates only. | Requires managing certificates for both clients and servers, often necessitating an internal Public Key Infrastructure (PKI). |
| Scalability                | Scales well for large numbers of users (e.g., public-facing websites). | Can be challenging to scale due to the need for managing numerous client certificates. |

Summary:

	•	TLS: Ensures secure, encrypted communication with server authentication, making it suitable for general web and application security.
	•	mTLS: Adds an extra layer of security by authenticating both parties, making it ideal for secure, trust-bound environments such as APIs or internal systems.

### Certificate Lifecycle

Certificates have a lifecycle that includes issuance, renewal, and eventual expiration. Proper management of this lifecycle is critical to maintaining secure communications and avoiding service interruptions.

### Trust Chains

The trustworthiness of a certificate is based on a **Trust Chain**. This begins with a Root Certificate (trusted by default in most operating systems and browsers) and extends to Intermediate and End-Entity Certificates. Each certificate in the chain vouches for the one directly below it.

## Common Use Cases

Digital certificates are crucial for various applications, including:

- **Website Security (HTTPS)**: Encrypting data transmitted between users and websites.
- **Email Security**: Verifying the identity of the sender and encrypting email content.
- **API and IoT Communication**: Ensuring secure communication between servers, APIs, and IoT devices.
- **Software Distribution**: Ensuring software authenticity and integrity through code-signing certificates.

## Resources

For more detailed information, refer to the following:

- [Mozilla's CA Certificate Program](https://wiki.mozilla.org/CA)
- [Let's Encrypt Documentation](https://letsencrypt.org/docs/)
- [SSL/TLS Best Practices by OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html)

---

## Contributing

Contributions are welcome! Please open an issue or submit a pull request if you would like to add new information or correct existing content.
