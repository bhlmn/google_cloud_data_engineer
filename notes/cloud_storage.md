# Cloud Storage

* GCS is elastic, meaning there is no limit to the size of the files on a bucket. As you place more data in there, it will scale to your needs.
* Buckets can be created on the cloud console GUI
* Interact with a bucket:
``` bash
gsutil ls gs://[bucket_name] # list contents of bucket
gsutil cp [file_name] gs://[bucket_name] # copy file from local to bucket
gsutil mb -p [project_name] -c [storage_class] -l [bucket_location] gs://[bucket_name] # create a bucket for a project in a specific location
```
* By default the data on a bucket is private. You can make it public by adding `allUsers` access to files or folders. This will make these public for everyone to see, and will provide a link for the files themselves.
* Storage classes. From standard storage —> near line —> cold line —> archive storage, you can balance the needs to reduce costs and how often you need to access a file.