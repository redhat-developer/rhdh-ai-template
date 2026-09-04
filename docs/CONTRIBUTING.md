# CONTRIBUTING

If you would like to contribute to the Software Templates on this repository, there are a few processes that you would need to follow. 

The Software Templates are found in the [../templates](../templates) directory and the reference reusable content are in the [../skeleton](../skeleton) directory.  The Software Templates are maintained by importing external resources. This allows the external resources to be standalone, developed independently, evolved and then imported.

This document addresses how you can contribute for 
- Pipelines
- GitOps
- AI Samples
- Software Templates
- Charts

## Pipelines

To update and/or contribute to the Pipelines, head over to the [rhdh-ai-template-pipelines](https://github.com/redhat-developer/rhdh-ai-template-pipelines) repository.

The [update-tekton-definition](../scripts/update-tekton-definition) script copies over the necessary resources from the rhdh-ai-template-pipelines repository into the [skeleton](../skeleton/) directory.

At this moment, the Software Templates support Tekton. All the Tekton resources - PipelineRun, Pipeline and Task are located in the rhdh-piplines repository.


## GitOps

The GitOps application is found in the [apps/ai](../apps/ai) directory. Changes are made here then used in the Software Template rendering process. See [apps/ai README](../apps/ai/README.md) for further details on GitOps usage/contribution.

The [apply-gitops-template](../scripts/apply-gitops-template) script copies over the necessary resources from the [apps/ai](../apps/ai) directory into the [skeleton](../skeleton/) directory.

At this moment, the Software Templates support ArgoCD.

## AI Samples

AI Samples are found in the [samples](../samples) directory. Changes are made here then used in the Software Template rendering process. The [pull-sample-apps.sh](../scripts/pull-sample-apps.sh) script can be used to pull upstream changes into the samples. See [samples README](../samples/README.md) for further details on samples usage/contribution.

The [apply-samples](../scripts/apply-samples) script copies over the necessary application files and resources into the the [templates](../templates/) directory. The script also copies over the necessary techdocs and the skeleton Software Template from the skeleton directory.

If you want to contribute to the techdocs associated with the Templates, check out the [techdoc](../skeleton/techdoc/) and [template-card-techdocs](../skeleton/template-card-techdocs/) directories.


## Software Templates

The base skeleton Software Template [template.yaml](../skeleton/template.yaml) is located in the skeleton directory. The skeleton template.yaml file is the main template file with gated logic for each Software Template. For example, the logic gated between `SED_LLM_LLAMA_SERVER_START` and `SED_LLM_LLAMA_SERVER_END` are only for a Llama model server Software Template. These gated conditions are applied in the [util](../scripts/util) script.

The ENV and properties for each Software Template are defined in the [envs](../scripts/envs/) directory. In this directory, each Software Template has their own file with the basic properties - name, description, model, model-server, etc. For instance, if you want to update a model being used in a Software Template, update these env files.

To generate Template updates based on your changes - Pipelines, GitOps, AI Samples, Software Template properties; run the [generate](../generate.sh) script: 

```
./generate.sh
```

This will generate all the Software Templates in the [templates](../templates/) directory based on your changes, which you can then commit to this repository.

## Charts

The Helm charts are found in the [charts](../charts) directory.

### External Tools

You will need to have the following tools installed to generate README and JSON Schema files from their respective templates.

#### Pre-Commit

Once this tool is installed you will need to run the `make install-pre-commit` to install the git pre-commit hook so that it will run and render the templates before you commit and push the changes in your pull request.

##### Description

Git hook scripts are useful for identifying simple issues before submission to code review. We run our hooks on every commit to automatically point out issues in code such as missing semicolons, trailing whitespace, and debug statements. By pointing these issues out before code review, this allows a code reviewer to focus on the architecture of a change while not wasting time with trivial style nitpicks.

##### Links

Website: [pre-commit.com](http://pre-commit.com/)  
Documentation: [pre-commit.com](http://pre-commit.com/)  
Example(s): [.pre-commit-config.yaml](https://github.com/backstage/charts/blob/main/.pre-commit-config.yaml)

#### Helm-Docs

##### Description

The helm-docs tool auto-generates documentation from helm charts into markdown files. The resulting files contain metadata about their respective chart and a table with each of the chart's values, their defaults, and an optional description parsed from comments.
The markdown generation is entirely Go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default README.md.gotmpl). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

##### Links

Repository: [norwoodj/helm-docs](https://github.com/norwoodj/helm-docs)  
Documentation: [README.md](https://github.com/norwoodj/helm-docs/blob/master/README.md)  
Example(s): [pre-commit-hook](https://github.com/backstage/charts/blob/main/.pre-commit-config.yaml#L2-L12)
