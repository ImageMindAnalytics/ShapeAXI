# Changelog

All notable changes to ShapeAXI are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.2] - 2026-05-25

### Fixed
- Removed the `grants` block from `.zenodo.json`. The NIH grants were not in
  Zenodo's awards index, which caused the InvenioRDM validator to reject the
  release deposit. Funding will be added through the Zenodo UI on the existing
  DOI record (edits do not change the minted DOI).

## [2.0.1] - 2026-05-25

### Added
- `CHANGELOG.md` and Zenodo integration for DOI minting on each tagged release.

## [2.0.0] - 2026-05-25

First release under the `ImageMindAnalytics` GitHub organization.

### Added
- Console entry points exposed in `[project.scripts]`:
  `saxi_folds`, `saxi_train`, `saxi_predict`, `saxi_eval`, `saxi_gradcam`,
  `split_train_eval`.
- MLflow logging support via `lightning.pytorch.loggers.MLFlowLogger`.
- New MLflow image-logging callbacks under `shapeaxi.saxi_logger`:
  `SaxiImageLoggerMLflow`, `SaxiImageLoggerMLflow_Ico_fs`,
  `SaxiImageLoggerMLflow_Ico_one_feature`, `SaxiAELoggerMLflow`,
  `SaxiDenoiseUnetLoggerMLflow`, `SaxiDDPMLoggerMLflow`,
  `SaxiClassLoggerMLflow`, `SaxiClassMHAFBLoggerMLflow`,
  `SaxiClassRingLoggerMLflow`, `SaxiNeRFLoggerMLflow`.
- `mlflow>=2.9` added to runtime dependencies.

### Changed
- Repository moved from `DCBIA-OrthoLab/ShapeAXI` to
  `ImageMindAnalytics/ShapeAXI`. The `Source Code` URL in project metadata
  and README links have been updated.
- The `shapeaxi` console script was renamed to `saxi_folds` to match its
  module name and align with the new entry points.

### Removed
- **Breaking**: Neptune logging support. `NeptuneLogger` is no longer imported
  (it was removed from `lightning.pytorch.loggers` in recent Lightning releases).
- **Breaking**: CLI flags `--neptune_project`, `--neptune_tags`, and
  `--neptune_token` are gone. Use `--mlflow_experiment_name`,
  `--mlflow_tracking_uri`, `--mlflow_run_name`, and `--mlflow_tags` instead.
- **Breaking**: `Saxi*LoggerNeptune` callback classes were renamed to
  `Saxi*LoggerMLflow`. CLI invocations passing the old class names via
  `--logger` must be updated.

### Migration notes
- Replace `--neptune_tags ...` with `--mlflow_experiment_name <name>` (this is
  the new gate that enables remote logging). Set `MLFLOW_TRACKING_URI` in the
  environment or pass `--mlflow_tracking_uri`.
- Rename any `--logger SaxiImageLoggerNeptune` (or similar) to
  `SaxiImageLoggerMLflow`.

## [1.1.1] and earlier

See the git history for releases prior to `2.0.0`.
