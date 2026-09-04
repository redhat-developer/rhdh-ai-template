## ai-software-templates

Apart from the [pipeline-install](./pipeline-install/) and the [pipeline-setup](./pipeline-setup/) which are tools to help you install the Tekton Pipelines along with your charts, the rest of charts under this directory are based on the [gitops resources app](../../../apps/ai/).

### Pull automatically latest changes

To pull all the latest changes for the charts from the [gitops resources app](../../../apps/ai/) you can simply run the `generate.sh` script placed in the root dir of this repository.

The script will copy the [gitops resources app](../../../apps/ai/) and will convert the necessary resources to Helm chart template files. Each chart has a corresponding `env` file under the `scripts/envs` dir which helps us configure the behavior of the conversion process.
