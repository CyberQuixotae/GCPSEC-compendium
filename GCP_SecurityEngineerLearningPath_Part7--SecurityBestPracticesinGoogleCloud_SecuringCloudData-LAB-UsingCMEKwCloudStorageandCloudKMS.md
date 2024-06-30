[Using Customer-Managed Encryption Keys with Cloud Storage and Cloud KMS](https://www.cloudskillsboost.google/paths/15/course_templates/87/labs/450298)

# Objectives

- In this lab, you will learn how to do the following:

- Manage keys and encrypted data using Cloud KMS.
- Create KeyRings and CryptoKeys.
- Set a default encryption key for a storage bucket.
- Encrypt an object with a Cloud KMS key.
- Rotate encryption keys.
- Perform server-side encryption manually with Cloud KMS keys.

### Create the Bucket
```bash
gsutil mb -l us gs://$DEVSHELL_PROJECT_ID-kms
```
- $DEVSHELL_PROJECT_ID refers to the project id that is set when running:
```bash
gcloud config set project [PROJECT_ID]
```
### Generate some files to transfer to our bucket
```bash
echo "This is sample file 1" > file1.txt
echo "This is sample file 2" > file2.txt
echo "This is sample file 3" > file3.txt
```

### Copy file1.txt to the bucket:
```bash
gsutil cp file1.txt gs://$DEVSHELL_PROJECT_ID-kms
```
### Enable Cloud KMS
```bash
gcloud services enable cloudkms.googleapis.com
```

### Create a KeyRing and CryptoKey
**Note:** In order to encrypt data, you need to create a **KeyRing** and a **CryptoKey**. KeyRings are useful for **grouping keys**. Keys can be grouped by environment (like test, staging, and prod) or by some other conceptual grouping. For this lab, your KeyRing will be called **test** and your CryptoKey will be called **labkey**.

- Variables to hold the KeyRing and CryptoKey name:
```bash
KEYRING_NAME=lab-keyring
CRYPTOKEY_1_NAME=labkey-1
CRYPTOKEY_2_NAME=labkey-2
```
- Create the KeyRing with:
```bash
gcloud kms keyrings create $KEYRING_NAME --location us
```

- Using the new KeyRing, create a CryptoKey named **labkey-1**:
```bash
gcloud kms keys create $CRYPTOKEY_1_NAME --location us \
--keyring $KEYRING_NAME --purpose encryption
```
- Create another CryptoKey named **labkey-2**:
```bash
gcloud kms keys create $CRYPTOKEY_2_NAME --location us \
--keyring $KEYRING_NAME --purpose encryption
```
### Add a default key for a bucket

- View default encryption key for your bucket:
```bash
gsutil kms encryption gs://$DEVSHELL_PROJECT_ID-kms
```
- Note: The bucket should not currently have a default encryption key. This means all data in the bucket will be encrypted by Google-managed encryption keys.

### Assign Cloud KMS keys to a service account
- Run the following commands to give your Cloud Storage service account permission to use both of your Cloud KMS keys:

```bash
gsutil kms authorize -p $DEVSHELL_PROJECT_ID -k \
projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\
/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME
gsutil kms authorize -p $DEVSHELL_PROJECT_ID -k \
projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\
/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_2_NAME
```

- The general syntax of the above commands is given below:
```bash
gsutil kms authorize -p [PROJECT_STORING_OBJECTS] -k [KEY_RESOURCE]
```
- Where `KEY_RESOURCE` is in the format:
```projects/[PROJECT_STORING_KEYS]/locations/[LOCATION]/keyRings/[KEY_RING_NAME]/cryptoKeys/[KEY_NAME]```

### Set the default key for a bucket

- Set the default key for your bucket to the first key you generated:
```bash
gsutil kms encryption -k \
projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\
/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME \
gs://$DEVSHELL_PROJECT_ID-kms
```
- View the default key for the bucket to verify
```bash
gsutil kms encryption gs://$DEVSHELL_PROJECT_ID-kms
```
- **Note: Objects that were written to a bucket prior to adding or changing the default key remain encrypted with the previous encryption method.**

- Copy **file2.txt** to the bucket:
```bash
gsutil cp file2.txt gs://$DEVSHELL_PROJECT_ID-kms
```

### View the files in the bucket
- In the Cloud Console, go to Navigation menu > Cloud Storage > Browser and click on your bucket for this lab.
- You will see file 1 was encrypted with a Google-managed key and file 2 was encrypted with a customer-managed key.

### Encrypt individual objects with a Cloud KMS key

In this task, you encrypt an individual object with a Cloud KMS key. This is useful if you want to use a different key from the default key set on the bucket, or if you don't have a default key set on the bucket. This can be done by passing the key to use in each gsutil command by using the -o flag:
`-o &#34;GSUtil:encryption_key=[KEY_RESOURCE]&#34;`

- Run the following command to copy file3.txt to the bucket, encrypting it with your second encryption key:
```bash
gsutil -o \
"GSUtil:encryption_key=projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\
/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_2_NAME" \
cp file3.txt gs://$DEVSHELL_PROJECT_ID-kms
```
### Identify the key used to encrypt an object

- Run the following command to display details about an object (the -L option causes gsutil ls to display all file details):
```bash
gsutil ls -L gs://$DEVSHELL_PROJECT_ID-kms/file3.txt
```
### Automatically rotate keys
Note: By providing a rotation schedule, Cloud KMS will automatically rotate your keys for you. A key's rotation schedule can be set using the gcloud command-line tool or via the Cloud Console.

### Manually rotate keys
Note: Manually rotating keys can also be done with the gcloud command-line tool or via the Cloud Console.

- In the Cloud Console, go back to the KeyRing named lab-keyring and click on the key named labkey-2 to view all versions.

- Click the Rotate Key button and then click Rotate.

You now have two versions of this key, version 2 is the primary one.

Note: Using the key rotation commands above, key rotation does NOT re-encrypt already encrypted data with the newly generated key version. If you suspect unauthorized use of a key, you should re-encrypt the data protected by that key and then disable or schedule destruction of the prior key version.

### Destroy old keys
Note: If you destroy a key that encrypts existing objects, you will be unable to recover that data, but you will continue to be charged for storage of your objects until you delete them.

### Bonus task. Encrypt data with the REST API

Run the following command to encode some sample text as base64 and store it in a variable named PLAIN_TEXT:
```bash
PLAIN_TEXT=$(echo -n "Some text to be encrypted" | base64)
```
Echo the PLAIN_TEXT variable to verify the text was encoded:
```bash
echo $PLAIN_TEXT
```
Use the REST API to encrypt the encoded text by calling the encrypt method of your key.

Supply the base64-encoded content in the plaintext field of the JSON for your request:
```bash
curl \
"https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME:encrypt" \
-d "{\"plaintext\":\"$PLAIN_TEXT\"}" \
-H "Authorization:Bearer $(gcloud auth application-default \
print-access-token)" \
-H "Content-Type: application/json"
```

The response will be a JSON payload containing the encrypted text in the ciphertext field:
```json
{
  "name": "projects/PROJECT_ID/locations/us/keyRings/lab-keyring/cryptoKeys/labkey-1/cryptoKeyVersions/1",
  "ciphertext": "CiQAdZkxhhrCJ/32gy9uBJBrJT1QvkEzkCcabVbx+yEMAdQtVYMSQgAtGz7vKsK93Yp2w8R82jnrWxkYh7t/3ZZE2JJyzC+X5rqJsDuk0C6R1PWHaEIuMSHEZfqV2d//zFSvHmSpdfgizg==",
  "ciphertextCrc32c": "3633892342",
  "protectionLevel": "SOFTWARE"
}
```
Note: The encrypted text can easily be extracted from the JSON response, and saved to a file by using the command-line utility **jq**. The response from the previous call can be piped into **jq**, which can parse out the **ciphertext** property and save to **data1.encrypted**.

Run the following command that repeats the encryption, but this time parses out the ciphertext property and saves it to the data1.encrypted file:
```bash
curl \
"https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME:encrypt" \
-d "{\"plaintext\":\"$PLAIN_TEXT\"}" \
-H "Authorization:Bearer $(gcloud auth application-default \
print-access-token)" \
-H "Content-Type: application/json" \
| jq .ciphertext -r > data1.encrypted
```
View the contents of the data1.encrypted file with the following command:
```bash
more data1.encrypted
```
Note: The encrypted text can be decrypted by calling the decrypt method of your key. You **must use** the same key that was used to encrypt the content.

Run the following command to decrypt the contents in the data1.encrypted file and save it into the file named data1.decrypted:
```bash
curl -v \
"https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME:decrypt" \
-d "{\"ciphertext\":\"$(cat data1.encrypted)\"}" \
-H "Authorization:Bearer $(gcloud auth application-default \
print-access-token)" \
-H "Content-Type:application/json" \
| jq .plaintext -r | base64 -d > data1.decrypted
```
View the contents of the data1.decrypted file with the following command:

```bash
more data1.decrypted
```

