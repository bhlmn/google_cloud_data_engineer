# Cloud Storage

## Public Datasets
Google Cloud hosts public datasets for analytical exploration and ingestion into machine learning models: https://cloud.google.com/public-datasets/.

* GCS is elastic, meaning there is no limit to the size of the files on a bucket. As you place more data in there, it will scale to your needs.
* Buckets can be created on the cloud console GUI
* By default the data on a bucket is private. You can make it public by adding `allUsers` access to files or folders. This will make these public for everyone to see, and will provide a link for the files themselves.
* Storage classes. From standard storage —> near line —> cold line —> archive storage, you can balance the needs to reduce costs and how often you need to access a file.