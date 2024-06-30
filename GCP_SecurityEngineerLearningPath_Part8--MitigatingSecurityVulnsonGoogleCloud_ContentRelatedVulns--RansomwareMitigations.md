[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/88/video/483861)

# Ransomware Mitigations
- Google Cloud provides multiple layers of protection against ransomware.
- Most protections are automated and available by default.

## Automtated mitigations
- Google has global visibility into malicious sites and content.
- This visibility makes the detection of incoming attacks very effective.

## End-user protection
- Gmail automatically prevents many malicious attacks from reaching inboxes.
- Google Safe Browsing identifies dangerous links.
- Google Drive scans files for malware.

## Data-related mitigations
- Make regular backups
- Use IAM best practices
- Use the Cloud Data Loss Prevention API

## Data-related mitigations: Backups
- Ransomware often targets backups to prevent data recovery.
- Having durable, secure backups can mitigate effects of ransomware.

## Data-related mitigations: IAM best practices
- **Restrict administrative access:**
    - Principle of least privilege
- **Restrict code execution:**
    - Use service accounts with appropriate roles

## Data-related mitigations: The Cloud Data Loss Prevention API
- Ensure that sensitive data is not accidentally exposed.
- Leverage the DLP API:
    - Scan all documents for sensitive data before publication.
