[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450294) <!--Increment the end number by 1 for the duration of each numbered section!-->

### Encryption overview
All data stored on Google Cloud is encrypted at rest by default.
- Includes data in **Storage, Persistent disks, Cloud SQL,**etc.
- Also includes disk snapshots and custom images.

#### Steps:
1. Data is uploaded to Google Cloud
2. Data is chunked and each chunk is encrypted with its own key
3. Chunks are distributed across Google's storage infrastructure

- Decrypting data requires the unwrapped data encryption key (DEK) for that data chunk.

### Encryption review
- All data stored on Google Cloud is encrypted at rest by default.
    - Includes data in Storage, Persistent disks, Cloud SQl, etc.
    - Also includes disk snapshots and custom images.

- All data in Google Cloud is encrypted with a unique data encryption key (DEK).
- DEKs are encrypted with ("wrapped" by) key encryption keys (KEKs) and stored with the data.
    - By default, KEKs are stored and used inside Keystore.
    - Decrypting data requires the unwrapped data encryption key (DEK) for that data chunk.

### Google Cloud encryption by default
- By default, KEKs are fully managed by Google.
- There is nothing to enable or configure.
- KEKs used by storage systems aren't exportable from Keystore
    - Prevent leaks and misuse, enabled Keystore to create an audit trail
- Keystore can automatically rotate KEKs at regular time intervals.
- Often refer to just a single key, really mean that data is protected using a key set

### Customer-managed encryption keys (CMEK)
- Allows you to manage the KEKs:
    - Generate keys
    - Rotation periods
    - Expire keys
- KEKs still stored on Cloud KMS.

### Creating keys with Cloud KMS
1. Create a key ring
2. Add a key
3. Specify type of key (symmetric, asymmetric, etc.)
4. Define rotating period

- Choose your managed key when creating VMs, disks, images, storage buckets, etc.
- Grant permissions to the service account to use your key.

### Customer-supplied keys
You can also create keys on premises. You are then responsible for all key management and rotation
- You must provide the key when creating or using the storage resource.
- Customer-supplied encryption keys (CSEK) allows you to use their own encryption keys to encrypt data at rest in Google Cloud.

#### GOOGLE WILL NOT STORE THE KEYS: DON'T LOSE THEM!!

### Cloud External Key Manager (Cloud EKM)
Protect data in Google Cloud using keys that you manage within a supported external key management partner.

**Key benefits:**
- Key provenance
- Access control
- Centralized key management
