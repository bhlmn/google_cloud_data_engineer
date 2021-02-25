# Compute Engine

By default these compute instances don’t come with anything on them. So you will probably have to start with:
``` bash
sudo apt-get install git
```
* A big idea with cloud-based tools is that compute and storage are separate.
* When you no longer need a VM, you can either stop it or delete it. When you stop it you no longer pay for the compute, but you /do pay/ for the storage attached to the VM (e.g., 10GB or so). Deleting the VM will completely wipe it away.
