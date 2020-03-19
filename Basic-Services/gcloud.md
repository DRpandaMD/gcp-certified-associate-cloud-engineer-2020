# The run down on gcloud


## Links to helpful Documentation

* [gcloud Overview](https://cloud.google.com/sdk/gcloud/)

* [gcloud Syntax](https://cloud.google.com/sdk/gcloud/reference/)

* [gcloud Properties](https://cloud.google.com/sdk/docs/properties)

* [gcloud Configurations](https://cloud.google.com/sdk/docs/configurations)

## Important Exam Info

* CLI tool for GCP

* Best friends with `gsutil` and `bq`

  * All share same configuration set via `gcloud config`

  * `gsutil` could have been `"gcloud storage"`

  * `bq` cloud have been `"gcloud bigquery"`

* In general more powerful than the console but less powerful than REST API

* Alpha and Beta versions are available via "`gcloud alpha`" or "`gcloud beta`"


### Basic Systnax

* `gcloud <global flags> <service/product> <group/area> <command> <flags> <parameters>`

* always drill down from left to right

* Examples: 

    * `gcloud --project myprojid compute instances list`

    * `gcloud --project=myprojid compute instances list`

    * `gcloud compute instances create myvm`

    * `gcloud services list --available`

    * `gsutil ls`

    * `gsutil mb -l northamerica-northeast1 gs://storage-lab-cli`

    * `gsutil label set bucketlabels.json gs://storage-lab-cli`

### Global Flags

* `--help`

* `-h`

* `--project <ProjectId>`

* `--account <Account>`

* `--filter` -- sometimes better than using grep 

* `--format`

  * Can choose between JOSN, YAML, CSV etc

  * Can pipe out JSON to `"jq"` command for further processing

* `--quiet` or `-q`


### Configuration Properties 

* Values entered once and used by any command that needs them

* Can be overridden on a specific command with corresponding flag

* Used very often for account, project, region, and zone

  * Set "core/account" or "account" to replace "--account"

  * Set "core/project" or "project" to replace "--project"

  * set "compute/region" to replace --region

  * set "compute/zone to replace --zone

* Set with `gcloud config set <property> <value>`

* check with `gcloud config get-value <property`

* clear with `gcloud config unset <property>`