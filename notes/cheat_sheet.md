# Cheat Sheet

## gsutils

``` bash
# list contents of a bucket
gsutil ls gs://[bucket_name]

# copy file from local to bucket
gsutil cp [file_name] gs://[bucket_name] # copy file from local to bucket

# create a bucket for a project in a specific location
gsutil mb -p [project_name] -c [storage_class] -l [bucket_location] gs://[bucket_name]
```