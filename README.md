# ComfyUI

A node-graph application for composing and executing generative image and other model workflows. Workflows connect model loaders, conditioning, samplers and output nodes.

## Architecture and stack

`main.py` starts the application; `server.py` exposes HTTP/WebSocket routes; `execution.py` schedules graph execution; `comfy/` owns inference and device/memory management; `custom_nodes/` extends the node catalogue.

## Requirements

Python >=3.10, PyTorch, aiohttp and compatible model/GPU dependencies. Models and GPU drivers are separate from the source tree.

## Installation and local development

This snapshot is incomplete: root `requirements.txt` is absent, although installation helpers expect it. Do not use `pip install .` as a substitute: `pyproject.toml` does not declare runtime dependencies. Recover the dependency manifest from the exact matching upstream revision before installing. After installing its dependencies and model files, the source entry point is `python main.py`.

## Configuration

Model search paths are configured using `extra_model_paths.yaml.example`. Keep model weights outside Git. Review custom nodes before enabling them; they execute Python locally.

## Testing

`pytest.ini` discovers `tests/` and `tests-unit/`. With the matching dependency/test environment installed, run `python -m pytest -m "not inference"`; inference tests additionally require model assets and hardware.

## Deployment and integrations

Run locally first. A deployment requires a compatible accelerator backend, persistent model/input/output storage and restricted access to the application server. `openapi.yaml` describes API operations.

## Source provenance and license

This repository imports source from [comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI). Original product functionality belongs to its upstream contributors. The local history begins with a November 2026 source snapshot; it does not retain upstream development history or prove the exact upstream revision. GitHub reports the upstream repository was created on 2023-01-17; that is repository-origin evidence, not the date of this contribution. Existing year folders are retained as local organization.

Preserve `LICENSE` and existing third-party notices when redistributing. Missing root license text was recovered from the upstream repository during this maintenance pass; existing license files were preserved.

## Validation status

Setup and test commands above were checked against this checkout’s manifests, scripts and entry points. Full dependency installation, application builds and integration tests were not performed in this maintenance pass. The default Python 3.9 is below the declared >=3.10 floor, and the root runtime requirements manifest is absent. No model files or GPU inference environment were provisioned. These instructions identify the supported workflow without claiming a successful product build.

See [source provenance](SOURCE_PROVENANCE.md) for pinned upstream license retrieval evidence and redistribution limitations.
