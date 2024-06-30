[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450299) <!--Increment the end number by 1 for the duration of each numbered section!-->

### What is an HSM (hardware security module)?
- An HSM is a physical device that manages digital keys.
- The HSM encrypts and decrypts data with secure cryptoprocessor chips.
- Using an HSM adds an extra layer of security to keys and data.

### Cloud HSM
- Cloud HSM provides an HSM hardware cluster that is managed and maintained by Google.
- Cloud HSM is available:
    - Across all US regions.
    - In multiple regions worldwide.
- Cloud HSM supports:
    - FIPS 140-2 level 3.
        - FIPS 140-2 is a US government computer security standard for cryptographic modules.
        - Level 3 includes tamper-evident physical security mechanisms and has a high probability of detecting and responding to attempts at physical access, use, or modification of the cryptographic module.
        - The physical security mechanisms may include the use of strong enclosures and tamper detection and response circuitry.
        - Cloud HSM supports Cavium version 1 and version 2 attestation formats.An attestation statement shows that the key is HSM-protected. It is a token that is cryptographically signed directly by the physical hardware and can be verified by the user.

### Cloud HSM leverages Cloud KMS
- Cloud HSM is fully integrated with Cloud KMS.
- For the Protection level, specify HSM.

### Attestation statements show that keys are protected
- For keys created in Cloud HSM, an attestation statement can be generated.
- The attestation statement:
    - Provides evidence that the key is HSM-protected.
    - Contains a token that is crytpographically signed directly by the physical hardware.
    - Can be verified by the user.


