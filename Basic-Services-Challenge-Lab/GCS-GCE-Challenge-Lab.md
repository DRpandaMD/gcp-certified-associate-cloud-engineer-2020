# GCS & GCE Challenge Lab

## Notes

### Desired End State

* A Brand new Project

* A GCE Instance that runs the provided script

* System Logs available in Stackdriver Logs

* A new GCS Bucket for resultling log files

* Log file appears in new bucket after instances finishes starting up

* No need to SSH to instance



### How to get there

* Make a new project (Pretty Easy)

* Make a new Bucket with Regional (cheap and also easy to do)

* Enable GCE -- note the APIs for GCE are not enabled by default.  BUT! By clicking on the GCE Tab will make an API Call to get those enabled.  (Just Remember that if you want to script this out for later)


* Go ahead and make the F1-micro

* In the start up script area copy and paste the below script into the window area.

* *note* see `log_bucket_metadata_name=lab-logs-bucket` here you are setting the name of the meta data field to `"lab-logs-bucket"`  

    * Copy that name, that is key for the metadata value

    * then you will want to copy and paste in `gs://<bucketname>/` format the bucket name into the value field

    * The author from acloudguru does a shit job explaining this

    * but basically at VM creation time you can create extra metadata for the VM that is user defined

    * you would then use that in the script

    * in the video has it in the script already which can be super confusing to watch

## Start up script used

```bash
#! /bin/bash

#
# Echo commands as they are run, to make debugging easier.
# GCE startup script output shows up in "/var/log/syslog" .
#
set -x


#
# Stop apt-get calls from trying to bring up UI.
#
export DEBIAN_FRONTEND=noninteractive


#
# Make sure installed packages are up to date with all security patches.
#
apt-get -yq update
apt-get -yq upgrade


#
# Install Google's Stackdriver logging agent, as per
# https://cloud.google.com/logging/docs/agent/installation
#
curl -sSO https://dl.google.com/cloudagents/install-logging-agent.sh
bash install-logging-agent.sh


#
# Install and run the "stress" tool to max the CPU load for a while.
#
apt-get -yq install stress
stress -c 8 -t 120


#
# Report that we're done.
#

# Metadata should be set in the "lab-logs-bucket" attribute using the "gs://mybucketname/" format.
log_bucket_metadata_name=lab-logs-bucket02
log_bucket_metadata_url="http://metadata.google.internal/computeMetadata/v1/instance/attributes/${log_bucket_metadata_name}"
worker_log_bucket=$(curl -H "Metadata-Flavor: Google" "${log_bucket_metadata_url}")

# We write a file named after this machine.
worker_log_file="machine-$(hostname)-finished.txt"
echo "Phew!  Work completed at $(date)" >"${worker_log_file}"

# And we copy that file to the bucket specified in the metadata.
echo "Copying the log file to the bucket..."
gsutil cp "${worker_log_file}" "${worker_log_bucket}"
```