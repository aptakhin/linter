# Linter

Open and available on Github Linter rules project.

# Using in project

Create file `pyproject.toml` with content:

```toml
[tool.flakeheaven]
base = "https://raw.githubusercontent.com/aptakhin/linter/main/pyproject.toml"
```

Everything below will override base rules.

## Installation

Flake plugin dependencies for `pipenv`:

```toml
# flakes
flake8 = "==4.0.1"
flake8-commas = "==2.1."
flakeheaven = "==3.1.0"
importlib-metadata = "<5.0"  # Fixes: https://stackoverflow.com/a/73932581
```
# Running

For start, can run with empty baseline, but file need to be exist.

```bash
touch .baseline
```

Run linter:

```bash
flakeheaven lint
```

Or to make baseline:

```bash
flakeheaven baseline > .baseline
```

If we want to ignore `E241` for some align `# noqa: E241`

```python
self.addTransformation([sx, 0,
                        0,  sy, # two spaces for aligning
                        0,  0]) # two spaces for aligning
```

Example:

```python
self.addTransformation([sx, 0,
                        0,  sy,  # noqa: E241
                        0,  0])  # noqa: E241
```

# VS Code integration

For underlining visible linter issues before commiting can configure `flake8heavened` with our configs for VS Code. 

Install VS Code extension: https://marketplace.visualstudio.com/items?itemName=ms-python.flake8
Pre-release extension (for 01.11.2022 release is unavailable yet).

`flake8heavened` - special version of compatible to flake8 binary `flakeheaven`.

Configure extension settings:

- _Flake8: ArgsSet_: `--relative`, it shows to treat absolute paths relative to baseline. Otherwise `flake8heavened` will ignore our baseline (and config).
- _Flake8: Import Strategy_: `fromEnvironment`
- _Flake8: Path_: Set absolute path to venv `flake8heavened`
 