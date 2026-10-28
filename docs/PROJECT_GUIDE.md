# TruthLens developer guide

TruthLens combines trained image classifiers, forensic signals, provenance inspection, and three presentation layers. Classification scores express model behavior on an input; neither a high score nor missing metadata proves an image's origin. The existing [project documentation](PROJECT_DOCUMENTATION.md) and [Swin evaluation](SWIN_MODEL_EVALUATION.md) describe training and evaluation in more detail.

## Install and choose an entry point

From the repository root, create the virtual environment before starting either interface:

```sh
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
```

The requirements declare minimum versions rather than a reproducible lock. PyTorch, torchvision, device drivers, and checkpoints must be compatible. Dataset downloads and training are separate, potentially expensive operations; neither is part of starting the UI.

| Interface | Entry point | Local address |
| --- | --- | --- |
| Original Streamlit | `.venv/bin/streamlit run app/app.py` | http://localhost:8501 |
| Alternate Streamlit | `.venv/bin/streamlit run frontend_v2/app.py` | Streamlit's printed address |
| Next.js plus Python API | Commands below | http://localhost:3000 |

For the Next.js interface:

```sh
.venv/bin/python -m pip install -r frontend_next/api/requirements.txt
cd frontend_next
npm ci
bash run.sh
```

The launcher starts Uvicorn on port 8000 and Next development on 3000. It expects the root `.venv`; stopping the launcher cleans up its API child. The root `run.sh` instead serves the original Streamlit interface and stops matching existing Streamlit processes, so use the explicit Streamlit command when you want to control each process independently.

## Architecture and assets

`src/` owns preprocessing, model construction, prediction, training, and evaluation. `app/inference.py` is the shared model registry and inference adapter. The Streamlit interfaces call it directly. `frontend_next/api/server.py` wraps it with FastAPI; Next route handlers proxy browser requests to that Python process through `frontend_next/lib/backend.ts`.

`models/` contains some artifacts, but not every model selectable in the registry is necessarily usable in a fresh clone. Check the registry's expected checkpoint paths, download instructions, and model-loading errors before treating a selection as available. Feature arrays under `features/` and dataset/diagnostic scripts support research; they are not a substitute for model weights. Keep evaluation splits and checkpoint provenance associated with the reported result.

## HTTP contract

The Python service provides:

| Method/path | Contract |
| --- | --- |
| `GET /health` | Process response with `status` and `service`; does not load every model |
| `GET /models` | Registry entries, keys, labels, Grad-CAM support, and available scores |
| `GET /benchmarks` | Model and resolution summaries from local evaluation artifacts |
| `POST /analyze` | Multipart `file`, `model_type` (default `swin_improved_ep6`), and `with_gradcam` (default false) |

Analysis returns `filename`, dimensions, `resolution_tier`, `model_type`, the shared prediction `result`, and a PNG data URL or null `heatmap`. Query `/models` for valid keys; unsupported Grad-CAM requests are disabled. Upload types are JPEG, PNG, WebP, and BMP. The backend enforces 25 MiB and 40 million pixels. Empty/invalid images and unknown models return 400, unsupported media 415, oversized images 413, and model-load/inference errors 500. Missing required multipart fields use FastAPI validation responses.

The browser uses Next `/api/analyze`, `/api/health`, and `/api/benchmarks`. Set server-side `TRUTHLENS_API_URL` to change the Python origin from `http://127.0.0.1:8000`. Transport failure at the analysis proxy returns 503. The Python CORS configuration lists local port-3000 origins; the same-origin Next proxy is the intended browser boundary.

## Verification and deployment

```sh
.venv/bin/python -m pytest
```

Tests are under `tests/`; model-dependent cases may need checkpoints or optional dependencies. Inspect collection/fixtures before running heavy inference. Frontend checks run from `frontend_next`: `npm run lint`, `npm run typecheck`, and `npm run build`. `npm start` serves the built Next application; the Python service remains a separate required process.

Deploy Python with access to model files and compatible compute, then configure the Next server's upstream and request limits/timeouts. The development `run.sh` uses reload and is a local launcher. Restrict public access and resource usage according to the deployment: the current inference API does not implement accounts or per-user quotas. A responding health endpoint does not establish checkpoint readiness or classification accuracy.

For 503, check the Python process and upstream address. For 500, inspect Python model-load logs and artifact paths. For rejected uploads, check actual media type, decoded image dimensions, and limits at every proxy. For slow first inference, distinguish model loading from steady-state processing. Preserve the advisory interpretation of forensic/provenance fields and the caveats in the existing evaluation documentation.

## Reference

- [Source and configuration reference](REFERENCE.md)
- [Contributing](../CONTRIBUTING.md)
