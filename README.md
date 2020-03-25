# Cloud Build sample

## memo

```
# local build
# https://cloud.google.com/cloud-build/docs/build-debug-locally?hl=ja

gcloud components install docker-credential-gcr
docker-credential-gcr configure-docker
gcloud components install cloud-build-local
cloud-build-local --help

# push / dryrunは gcloud buildsにはない
cloud-build-local --config=cloudbuild-android-img.yaml \
  --dryrun=false \
  --substitutions _ANDROID_VERSION=29 \
  --push \
  ./docker_files


gcloud builds submit --config=cloudbuild-android-img.yaml \
  --substitutions _ANDROID_VERSION=29 \
  ./docker_files

# n1-standard-1 / n1-highcpu-8
gcloud builds submit --config=cloudbuild.yaml \
  --substitutions \
  _ANDROID_VERSION=29,_FLAVOR=Debug \
  --machine-type=n1-highcpu-32 \
  .
  
```


## ref

- https://cloud.google.com/cloud-build/docs/build-debug-locally
- https://cloud.google.com/cloud-build/docs/build-config
- https://cloud.google.com/cloud-build/docs/building/store-build-artifacts

