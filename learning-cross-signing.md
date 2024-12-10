# OpenSSL Tutorial: Creating Certificates and Cross-Signing

## Step 1: Create a Root Certificate Authority (Root CA A)

1. **Generate the Root Private Key**:
   ```bash
   openssl genrsa -out rootA.key 4096
   ```

2. **Create the Root Certificate**:
   ```bash
   openssl req -x509 -new -nodes -key rootA.key -sha256 -days 3650 -out rootA.crt \
       -subj "/C=US/ST=State/L=City/O=RootA Organization/OU=IT Department/CN=RootA"
   ```

---

## Step 2: Create a Second Root Certificate Authority (Root CA B)

1. **Generate the Second Root Private Key**:
   ```bash
   openssl genrsa -out rootB.key 4096
   ```

2. **Create the Second Root Certificate**:
   ```bash
   openssl req -x509 -new -nodes -key rootB.key -sha256 -days 3650 -out rootB.crt \
       -subj "/C=US/ST=State/L=City/O=RootB Organization/OU=IT Department/CN=RootB"
   ```

---

## Step 3: Create an Intermediate Certificate Authority under Root CA B

1. **Generate the Intermediate Private Key**:
   ```bash
   openssl genrsa -out intermediateB.key 4096
   ```

2. **Create a Certificate Signing Request (CSR) for the Intermediate Certificate**:
   ```bash
   openssl req -new -key intermediateB.key -out intermediateB.csr \
       -subj "/C=US/ST=State/L=City/O=IntermediateB Organization/OU=IT Department/CN=IntermediateB"
   ```

3. **Sign the Intermediate Certificate Using Root CA B**:
   ```bash
   openssl x509 -req -in intermediateB.csr -CA rootB.crt -CAkey rootB.key \
       -CAcreateserial -out intermediateB.crt -days 1825 -sha256
   ```

---

## Step 4: Create an End-Entity Certificate

1. **Generate the End-Entity Private Key**:
   ```bash
   openssl genrsa -out endEntity.key 2048
   ```

2. **Create a CSR for the End-Entity Certificate**:
   ```bash
   openssl req -new -key endEntity.key -out endEntity.csr \
       -subj "/C=US/ST=State/L=City/O=EndEntity Organization/OU=Web Department/CN=www.example.com"
   ```

3. **Sign the End-Entity Certificate Using Intermediate CA B**:
   ```bash
   openssl x509 -req -in endEntity.csr -CA intermediateB.crt -CAkey intermediateB.key \
       -CAcreateserial -out endEntity.crt -days 825 -sha256
   ```

---

## Step 5: Cross-Sign Root CA B with Root CA A

1. **Cross-Sign Root CA B**:
   ```bash
   openssl x509 -in rootB.crt -CA rootA.crt -CAkey rootA.key \
    -CAcreateserial -out rootB_cross_signed.crt -days 3650 -sha256
   ```

---

## Step 6: Verify the Certificates

1. **Erstellen der Zertifikatskette für das End-Entity-Zertifikat mit cross-signiertem Root CA B:**

   Kombiniere das Intermediate-Zertifikat und das cross-signierte Root-Zertifikat:
   ```bash
   cat intermediateB.crt rootB_cross_signed.crt > chainB_cross_signed.pem
   ```

2. **Validieren der End-Entity-Zertifikatskette mit dem cross-signierten Zertifikat:**
   ```bash
   openssl verify -CAfile chainB_cross_signed.pem endEntity.crt
   ```

   **Erläuterung:**
   - `chainB_cross_signed.pem`: Enthält die Intermediate CA und das cross-signierte Root CA B.
   - `endEntity.crt`: Das End-Entity-Zertifikat wird validiert.

3. **Verifizieren, dass der Client auf Root CA A schließt:**
   Wenn **Root CA A** im Trust Store des Clients vorhanden ist, wird die Verbindung als vertrauenswürdig akzeptiert, da die Kette zu **Root CA A** führt.

---

## Warum ist das wichtig?
- Die standardmäßige Kette (ohne `rootB_cross_signed.crt`) würde fehlschlagen, wenn der Client Root CA B nicht direkt vertraut.
- Mit `rootB_cross_signed.crt` wird sichergestellt, dass der Client die Verbindung validieren kann, auch wenn er nur Root CA A vertraut.

---

## Step 7: View Certificate Details

To view details of any certificate:
```bash
openssl x509 -in <certificate>.crt -text -noout
```

Replace `<certificate>` with:
- `rootA`
- `rootB`
- `intermediateB`
- `endEntity`
- `rootB_cross_signed`

---

## Key Files Generated

| **File**                  | **Description**                                          |
|---------------------------|----------------------------------------------------------|
| `rootA.key`               | Private key for Root CA A.                               |
| `rootA.crt`               | Certificate for Root CA A.                               |
| `rootB.key`               | Private key for Root CA B.                               |
| `rootB.crt`               | Certificate for Root CA B.                               |
| `intermediateB.key`       | Private key for Intermediate CA B.                       |
| `intermediateB.crt`       | Certificate for Intermediate CA B.                       |
| `endEntity.key`           | Private key for the end-entity (e.g., `www.example.com`).|
| `endEntity.crt`           | Certificate for the end-entity.                          |
| `rootB_cross_signed.crt`  | Cross-signed certificate for Root CA B.                  |
| `chainB_cross_signed.pem` | Zertifikatskette mit Intermediate CA B und cross-signiertem Root CA B. |