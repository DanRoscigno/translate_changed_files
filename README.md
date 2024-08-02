# translate_changed_files

1. Detect changed Markdown or MDX files using [tj-actions/changed-files](https://github.com/tj-actions/changed-files)
2. Translate Docusaurus Markdown from English to Chinese using [tcapelle/gpt_translate](https://github.com/tcapelle/gpt_translate)
3. Automatically open a PR with the Chinese docs using [peter-evans/create-pull-request](https://github.com/peter-evans/create-pull-request)

## Setup

### Github Personal Access Token

I used a fine-grained token limited to this repo. Here are the perms I gave:

- Read and Write access to code (content) and pull requests
- Read and Write access to pull requests

Additionally, GitHub automatically assigned:

- Read access to metadata

### Repository secret

I created three repository secrets:

### TRANSLATE_PAT

This contains the PAT created above.

### OPENAI_API_KEY

This contains a GPT4 API key

### WANDB_API_KEY

This contains the output of [W&B authorize](https://wandb.ai/authorize)

## Workflow file notes

- The [workflow](.github/workflows/translate.yml) runs when a pull request with target `main` is closed by being merged. It does not run on every commit made to a PR as that is wasteful.
- The paths and filters in the workflow are specific to the StarRocks docs, you will need to change them.

## `gpt_translate` configuration

The configuration is in the `configs` dir in this repo. At StarRocks we use a modified prompt and temperature in addition to a custom glossary in `configs/language_dicts/zh.yaml`. You can compare our prompt with the default from [tcapelle/gpt_translate](https://github.com/tcapelle/gpt_translate).

## About Weights and Biases

You should read [Weights & Biases](https://wandb.ai/site), I am no expert. I do think that the Weave feature is going to be useful as I tune the prompt and glossary I am using. Weave keeps track of the changes and the impact. Additionally, W&B validates the translations for me automatically and provides scores. Seriously, I am no AI expert; check out their site.
