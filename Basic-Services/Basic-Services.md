# Basic Services

## GCS: Google Cloud Storage 

* [Google Storage : Making Data Public](https://cloud.google.com/storage/docs/access-control/making-data-public)

* [Google Storage: bucket locations](https://cloud.google.com/storage/docs/bucket-locations)

* In this lab I included a `./lab-content/` directory that has a empty text file and some memes I enjoy to upload, edit permissions, move and delete in the cloud.  Feel Free to use them as you like.


### GSC: Google Cloud Storage (gsutil cli)

```bash
pwd
ls

gcloud config list

gsutil ls
gsutil ls gs://storage-lab-console/
gsutil ls gs://storage-lab-console/**

gsutil mb --help

gsutil mb -l northamerica-northeast1 gs://storage-lab-cli
gsutil ls

gsutil label get gs://storage-lab-console/
gsutil label get gs://storage-lab-console/ >bucketlabels.json
cat bucketlabels.json

gsutil label get gs://storage-lab-cli/
gsutil label set bucketlabels.json gs://storage-lab-cli/
gsutil label get gs://storage-lab-cli/

gsutil label ch -l "extralabel:extravalue" gs://storage-lab-cli

gsutil versioning get gs://storage-lab-cli/
gsutil versioning set on gs://storage-lab-cli/
gsutil versioning get gs://storage-lab-cli/

gsutil ls gs://storage-lab-cli/
gsutil cp README-cloudshell.txt gs://storage-lab-cli/
gsutil ls gs://storage-lab-cli/

gsutil ls gs://storage-lab-cli/
gsutil ls -a gs://storage-lab-cli/
gsutil rm gs://storage-lab-cli/README-cloudshell.txt
gsutil ls gs://storage-lab-cli/
gsutil ls -a gs://storage-lab-cli/

gsutil cp gs://storage-lab-console/** gs://storage-lab-cli/
gsutil ls gs://storage-lab-cli/
gsutil ls -a gs://storage-lab-cli/

gsutil acl ch -u AllUsers:R gs://storage-lab-cli/Selfie.jpg
```
