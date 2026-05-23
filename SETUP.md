# Sudoku-Bench teammate setup

## Prerequisites
- Python 3.10+
- `uv` installed and available on your PATH
- At least one model provider API key

## 1. Create the local environment
From the workspace root:

```powershell
uv venv .venv
```

Activate it:

```powershell
.\.venv\Scripts\Activate.ps1
```

## 2. Install dependencies
Install the eval dependencies:

```powershell
uv pip install -r .\Sudoku-Bench\src\eval\requirements.txt
```

If `vllm` fails on Windows, install the rest individually and skip `vllm` unless you are running on a supported Linux GPU environment:

```powershell
uv pip install aiohttp anthropic datasets jinja2 openai pandas tqdm transformers seaborn google-genai
```

## 3. Configure environment variables
Copy the example file:

```powershell
Copy-Item .\Sudoku-Bench\src\eval\.env.example .\Sudoku-Bench\src\eval\.env
```

Then edit `.\Sudoku-Bench\src\eval\.env` and fill in the provider key you need.

The local dataset already lives at:

```text
Sudoku-Bench/src/dataset/
```

That folder should contain:
- `challenge_100`
- `nikoli_100`
- `ctc`

## 4. Smoke test with the local dataset
From `Sudoku-Bench\src`, run a 1-row test:

```powershell
python -m eval.run `
  --dataset challenge_100 `
  --dataset_root .\dataset `
  --iloc_start 0 `
  --iloc_end 1 `
  --api custom_openai `
  --base_url https://your-provider.example.com/v1 `
  --api_key_env CUSTOM_API_KEY `
  --model your-model-name `
  --output_csv .\eval\smoke_test.csv `
  --batch_size 1
```

## 5. Run a full benchmark
Example using a custom OpenAI-compatible provider:

```powershell
python -m eval.run `
  --dataset challenge_100 `
  --dataset_root .\dataset `
  --api custom_openai `
  --base_url https://your-provider.example.com/v1 `
  --api_key_env CUSTOM_API_KEY `
  --model your-model-name `
  --output_csv .\eval\results\challenge_100\your-model-name.csv `
  --batch_size 16
```

## 6. Run sharded jobs in parallel
Example for shard 0 of 3:

```powershell
python -m eval.run `
  --dataset challenge_100 `
  --dataset_root .\dataset `
  --api custom_openai `
  --base_url https://your-provider.example.com/v1 `
  --api_key_env CUSTOM_API_KEY `
  --model your-model-name `
  --output_csv .\eval\results\challenge_100\your-model-name-shard0.csv `
  --num_shards 3 `
  --shard_idx 0 `
  --batch_size 16
```

Repeat with `--shard_idx 1` and `--shard_idx 2` on the other workers.

## 7. Verify imports
After installation, this should succeed:

```powershell
python -c "import openai, datvasets, pandas"
```

## Notes
- Use `--dataset_root .\dataset` when running from `Sudoku-Bench\src`.
- If you run from a different working directory, pass the dataset path relative to that directory or use an absolute path.
- Without `--dataset_root`, the runner falls back to the Hugging Face dataset.
