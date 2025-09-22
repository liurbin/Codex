# Using Azure OpenAI with Codex

This document shows how to use **Azure OpenAI** with Codex — i.e. how to configure Codex so that it works with your Azure OpenAI deployment.

---

## 1. Prerequisites

- Have an Azure OpenAI account  
- Have created a deployment (for example, gpt-5) in the Azure portal  

---

## 2. Installation

Install the `@openai/codex` package globally via npm:

```bash
npm i -g @openai/codex
```

After installation, verify it works by running:

```bash
codex --help
```

---

## 3. Configuration (`config.toml`)

In the root of your project, create or modify `config.toml`, directly putting in your Key:

```toml
[model_providers.azure]
name = "Azure"
base_url = "https://<your-resource-name>.openai.azure.com/"
# if not work, try like this: https://<your-resource-name>.openai.azure.com/openai/deployments/gpt-5
api_key = "your-azure-openai-key"     # write the Key directly
query_params = { api-version = "2025-04-01-preview" }
wire_api = "chat"

[profiles.azure_gpt]
model_provider = "azure"
model = "gpt-5"
preferred_auth_method = "apikey"

model_reasoning_effort = "high"
model_reasoning_summary = "detailed"
```

---

## 4. Usage

To start codex with the profile you configured:

```bash
codex --profile azure_gpt
```

---

## 5. Tips & Notes

- Ensure that `base_url` is the **Azure OpenAI resource endpoint** (e.g. `https://<your-resource-name>.openai.azure.com/`)  
- Do **not** expose your API key publicly. If you're planning to publish your project, replace your key with a placeholder like `"your-azure-openai-key"` in the config file.  

---
