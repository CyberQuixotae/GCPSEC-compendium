[Link to Lesson:](https://www.cloudskillsboost.google/paths/15/course_templates/87/video/450293) <!--Increment the end number by 1 for the duration of each numbered section!-->

# Signed URLs and policy documents

### Signed URLs
Allow access to Cloud Storage **without adding** a user to an ACL or IAM:
- **Benefit:** does not require your users to have a Google account in order to access Cloud Storage
- Temporary access with a timeout.
- Anyone with the signed URL has access.

### Create a signed URL with gsutil
1. Create a service account with rights to storage.
2. Create a service account key.
```shell
gcloud iam service-accounts keys create ~/key.json --iam-account storage-admin-sa@doug-demo-project.iam.gserviceaccount.com
```
3. Use signurl command, which returns a URL to allows access to the resource.
```shell
gcloud iam service-accounts keys create ~/key.json --iam-account storage-admin-sa@doug-demo-project.iam.gserviceaccount.com

gsutil signurl -d 10m ~/key.json gs://super-secure-bucket/noir.jpg
```

### Signed URL example

```https://storage.googleapis.com/example-bucket/cat.jpeg?X-Goog-Algorithm=
GOOG4-RSA-SHA256&X-Goog-Credential=example%40example-project.iam.gserviceaccount
.com%2F20181026%2Fus-central1%2Fstorage%2Fgoog4_request&X-Goog-Date=20181026T18
1309Z&X-Goog-Expires=900&X-Goog-SignedHeaders=host&X-Goog-Signature=247a2aa45f16
9edf4d187d54e7cc46e4731b1e6273242c4f4c39a1d2507a0e58706e25e3a85a7dbb891d62afa849
6def8e260c1db863d9ace85ff0a184b894b117fe46d1225c82f2aa19efd52cf21d3e2022b3b868dc
c1aca2741951ed5bf3bb25a34f5e9316a2841e8ff4c530b22ceaa1c5ce09c7cbb5732631510c2058
0e61723f5594de3aea497f195456a2ff2bdd0d13bad47289d8611b6f9cfeef0c46c91a455b94e90a
66924f722292d21e24d31dcfb38ce0c0f353ffa5a9756fc2a9f2b40bc2113206a81e324fc4fd6823
a29163fa845c8ae7eca1fcf6e5bb48b3200983c56c5ca81fffb151cca7402beddfc4a76b13344703
2ea7abedc098d2eb14a7
```

### Signed Policy Documents
- Signed Policy Documents specify what can be uploaded to a bucket with a form POST.
- Allow greater control over size, content type, and other upload characteristics than signed URLs.
- Created as JavaScript Object Notation (JSON).

### Signed Policy Document example
```json
{"expiration": "2020-06-16T11:11:11Z",
 "conditions": [
  ["starts-with", "$key", ""],
  {"bucket": "travel-maps"},
  {"success_action_redirect": "http://www.example.com/success_notification.html"},
  ["eq", "$Content-Type", "image/jpeg"],
  ["content-length-range", 0, 1000000],
  {"x-goog-algorithm": "GOOG4-RSA-SHA256"},
  {"x-goog-credential": "example_account@example_project.iam.gserviceaccount.com/20191102/us-central1/storage/goog4_request"},
  {"x-goog-date": "20191102T043530Z"}
  ]
}
```

### Using Policy Documents
1. Ensure the policy document is UTF-8 encoded.
2. Encode the policy document as a Base64 representation.
3. Sign your policy document using RSA with SHA-256 using the secret key provided to you in the Google Cloud console.
4. Encode the message digest as a Base64 representation.
5. Add the policy document information to the HTML form.


