# Truthlens source reference

Source reviewed: [`7d2e4496cd45`](https://github.com/noel-ult/Truthlens/commit/7d2e4496cd459361bf387c32c563cfe8b7f776c4).

This reference records the checked-in source, scripts, configuration names, and route declarations. It is a navigation aid; service availability and successful test execution require separate verification.

## Package commands

Run each command in the directory containing its package manifest. A declared script is not necessarily a passing check; guides call out placeholders and known mismatches.

### frontend_next/package.json

| Script | Shell command |
| --- | --- |
| `dev` | `next dev --turbopack` |
| `build` | `next build` |
| `start` | `next start` |
| `lint` | `eslint .` |
| `typecheck` | `tsc --noEmit` |

Manifest: [frontend_next/package.json](../frontend_next/package.json).

## Configuration names

Names below are declared by source or example files. Example-only entries may be stale; consult the linked reader and project guide before relying on them. Secret values are intentionally omitted.

| Name | Declared/read in |
| --- | --- |
| `PYTHONHASHSEED` | [src/utils.py](../src/utils.py) |
| `TMPDIR` | [scripts/upload_datasets_to_kaggle.py](../scripts/upload_datasets_to_kaggle.py) |
| `TRUTHLENS_API_URL` | [frontend_next/lib/backend.ts](../frontend_next/lib/backend.ts) |

## HTTP route declarations

Paths are **as declared in each source file**. Router/blueprint mount prefixes from the entry point must be prepended; the project guide describes the active entry point and common prefixes. Alternate entry points (such as SQLite) are listed separately by file. Authentication, request bodies, and response schemas live in the linked handlers/models.

| Source | Method | Declared path | Handler |
| --- | --- | --- | --- |
| [frontend_next/api/server.py](../frontend_next/api/server.py) | GET | `/health` | `health` |
| [frontend_next/api/server.py](../frontend_next/api/server.py) | GET | `/models` | `models` |
| [frontend_next/api/server.py](../frontend_next/api/server.py) | GET | `/benchmarks` | `benchmarks` |
| [frontend_next/api/server.py](../frontend_next/api/server.py) | POST | `/analyze` | `analyze` |

## File-based pages and handlers

- [frontend_next/app/api/analyze/route.ts](../frontend_next/app/api/analyze/route.ts)
- [frontend_next/app/api/benchmarks/route.ts](../frontend_next/app/api/benchmarks/route.ts)
- [frontend_next/app/api/health/route.ts](../frontend_next/app/api/health/route.ts)
- [frontend_next/app/page.tsx](../frontend_next/app/page.tsx)

## Existing documentation

Historical plans/reports describe their own revision; use current source when they disagree.

- [.agents/rules/main.md](../.agents/rules/main.md)
- [README.md](../README.md)
- [RETRAIN_PLAN.md](../RETRAIN_PLAN.md)
- [docs/PROJECT_DOCUMENTATION.md](../docs/PROJECT_DOCUMENTATION.md)
- [docs/SWIN_MODEL_EVALUATION.md](../docs/SWIN_MODEL_EVALUATION.md)
- [frontend_next/AGENTS.md](../frontend_next/AGENTS.md)
- [frontend_next/CLAUDE.md](../frontend_next/CLAUDE.md)
- [frontend_next/README.md](../frontend_next/README.md)
- [frontend_next/api/requirements.txt](../frontend_next/api/requirements.txt)
- [frontend_v2/README.md](../frontend_v2/README.md)
- [requirements.txt](../requirements.txt)

## Source and configuration map

Generated lockfiles, binary assets, compiled output, vendored dependencies, and cached bytecode are omitted. Test files remain listed so coverage can be located.

- [.streamlit/config.toml](../.streamlit/config.toml)
- [app/__init__.py](../app/__init__.py)
- [app/app.py](../app/app.py)
- [app/inference.py](../app/inference.py)
- [app/theme.py](../app/theme.py)
- [conftest.py](../conftest.py)
- [dataset/build_internet_testset.py](../dataset/build_internet_testset.py)
- [dataset/build_multires_dataset.py](../dataset/build_multires_dataset.py)
- [dataset/build_swin_union_manifest.py](../dataset/build_swin_union_manifest.py)
- [dataset/build_web_testset.py](../dataset/build_web_testset.py)
- [dataset/collect_modern_generators.py](../dataset/collect_modern_generators.py)
- [dataset/create_combined_dataset.py](../dataset/create_combined_dataset.py)
- [dataset/download_architecture_dataset.py](../dataset/download_architecture_dataset.py)
- [dataset/download_cifake.py](../dataset/download_cifake.py)
- [dataset/download_corpus.py](../dataset/download_corpus.py)
- [dataset/download_dalle_dataset.py](../dataset/download_dalle_dataset.py)
- [dataset/download_hf_cifake.py](../dataset/download_hf_cifake.py)
- [dataset/download_highres_150k.py](../dataset/download_highres_150k.py)
- [dataset/download_highres_dataset.py](../dataset/download_highres_dataset.py)
- [dataset/download_highres_master.py](../dataset/download_highres_master.py)
- [dataset/download_master_dataset.py](../dataset/download_master_dataset.py)
- [dataset/download_pure_dalle3.py](../dataset/download_pure_dalle3.py)
- [dataset/ingest_diffusion_and_real.py](../dataset/ingest_diffusion_and_real.py)
- [dataset/prepare_custom_dataset.py](../dataset/prepare_custom_dataset.py)
- [dataset/prepare_generator_dataset.py](../dataset/prepare_generator_dataset.py)
- [dataset/prepare_legacy_archive.py](../dataset/prepare_legacy_archive.py)
- [dataset/verify_swin_dataset.py](../dataset/verify_swin_dataset.py)
- [diag_app_paths.py](../diag_app_paths.py)
- [diag_benchmark.py](../diag_benchmark.py)
- [diag_content_genre.py](../diag_content_genre.py)
- [diag_corpus_audit.py](../diag_corpus_audit.py)
- [diag_eval_all.py](../diag_eval_all.py)
- [diag_forensics.py](../diag_forensics.py)
- [diag_modern_baseline.py](../diag_modern_baseline.py)
- [diag_recompress_skew.py](../diag_recompress_skew.py)
- [diag_shortcut_probe.py](../diag_shortcut_probe.py)
- [diag_strategy.py](../diag_strategy.py)
- [diag_swin_checkpoint_audit.py](../diag_swin_checkpoint_audit.py)
- [diag_tta_weighting.py](../diag_tta_weighting.py)
- [features/clip_vitl14/holdout__index.json](../features/clip_vitl14/holdout__index.json)
- [features/clip_vitl14/test__index.json](../features/clip_vitl14/test__index.json)
- [features/clip_vitl14/train__index.json](../features/clip_vitl14/train__index.json)
- [features/clip_vitl14/val__index.json](../features/clip_vitl14/val__index.json)
- [frontend_next/api/__init__.py](../frontend_next/api/__init__.py)
- [frontend_next/api/requirements.txt](../frontend_next/api/requirements.txt)
- [frontend_next/api/server.py](../frontend_next/api/server.py)
- [frontend_next/app/api/analyze/route.ts](../frontend_next/app/api/analyze/route.ts)
- [frontend_next/app/api/benchmarks/route.ts](../frontend_next/app/api/benchmarks/route.ts)
- [frontend_next/app/api/health/route.ts](../frontend_next/app/api/health/route.ts)
- [frontend_next/app/globals.css](../frontend_next/app/globals.css)
- [frontend_next/app/layout.tsx](../frontend_next/app/layout.tsx)
- [frontend_next/app/page.tsx](../frontend_next/app/page.tsx)
- [frontend_next/components/analysis-result.tsx](../frontend_next/components/analysis-result.tsx)
- [frontend_next/components/analyzer.tsx](../frontend_next/components/analyzer.tsx)
- [frontend_next/components/app-header.tsx](../frontend_next/components/app-header.tsx)
- [frontend_next/components/app-shell.tsx](../frontend_next/components/app-shell.tsx)
- [frontend_next/components/benchmarks.tsx](../frontend_next/components/benchmarks.tsx)
- [frontend_next/components/method.tsx](../frontend_next/components/method.tsx)
- [frontend_next/components/theme-toggle.tsx](../frontend_next/components/theme-toggle.tsx)
- [frontend_next/eslint.config.mjs](../frontend_next/eslint.config.mjs)
- [frontend_next/lib/backend.ts](../frontend_next/lib/backend.ts)
- [frontend_next/lib/models.ts](../frontend_next/lib/models.ts)
- [frontend_next/lib/types.ts](../frontend_next/lib/types.ts)
- [frontend_next/next-env.d.ts](../frontend_next/next-env.d.ts)
- [frontend_next/next.config.ts](../frontend_next/next.config.ts)
- [frontend_next/package.json](../frontend_next/package.json)
- [frontend_next/postcss.config.mjs](../frontend_next/postcss.config.mjs)
- [frontend_next/tsconfig.json](../frontend_next/tsconfig.json)
- [frontend_v2/.streamlit/config.toml](../frontend_v2/.streamlit/config.toml)
- [frontend_v2/__init__.py](../frontend_v2/__init__.py)
- [frontend_v2/app.py](../frontend_v2/app.py)
- [frontend_v2/theme.py](../frontend_v2/theme.py)
- [notebooks/01_EDA.py](../notebooks/01_EDA.py)
- [notebooks/02_Classical_ML.py](../notebooks/02_Classical_ML.py)
- [notebooks/03_CNN_Training.py](../notebooks/03_CNN_Training.py)
- [notebooks/04_GradCAM_Demo.py](../notebooks/04_GradCAM_Demo.py)
- [requirements.txt](../requirements.txt)
- [scripts/upload_datasets_to_kaggle.py](../scripts/upload_datasets_to_kaggle.py)
- [src/__init__.py](../src/__init__.py)
- [src/adapt_head.py](../src/adapt_head.py)
- [src/download_weights.py](../src/download_weights.py)
- [src/eval_protocol.py](../src/eval_protocol.py)
- [src/eval_swin.py](../src/eval_swin.py)
- [src/evaluate.py](../src/evaluate.py)
- [src/evaluate_generators.py](../src/evaluate_generators.py)
- [src/extract_grok_aurora.py](../src/extract_grok_aurora.py)
- [src/features_clip.py](../src/features_clip.py)
- [src/finetune_swin_hardstyles.py](../src/finetune_swin_hardstyles.py)
- [src/image_forensics.py](../src/image_forensics.py)
- [src/predict.py](../src/predict.py)
- [src/preprocessing.py](../src/preprocessing.py)
- [src/score_clip.py](../src/score_clip.py)
- [src/train.py](../src/train.py)
- [src/train_classical.py](../src/train_classical.py)
- [src/train_head.py](../src/train_head.py)
- [src/train_swin.py](../src/train_swin.py)
- [src/utils.py](../src/utils.py)
- [tests/__init__.py](../tests/__init__.py)
- [tests/test_architecture_dataset.py](../tests/test_architecture_dataset.py)
- [tests/test_collector_provenance.py](../tests/test_collector_provenance.py)
- [tests/test_custom_dataset.py](../tests/test_custom_dataset.py)
- [tests/test_download_corpus.py](../tests/test_download_corpus.py)
- [tests/test_eval_protocol.py](../tests/test_eval_protocol.py)
- [tests/test_image_forensics.py](../tests/test_image_forensics.py)
- [tests/test_predict.py](../tests/test_predict.py)
- [tests/test_preprocessing.py](../tests/test_preprocessing.py)
- [tests/test_swin_manifest.py](../tests/test_swin_manifest.py)
- [tests/test_swin_train_eval.py](../tests/test_swin_train_eval.py)
- [tests/test_train.py](../tests/test_train.py)
- [tests/test_verify_swin_dataset.py](../tests/test_verify_swin_dataset.py)
