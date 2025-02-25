# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


#### [1.5.2] - 2021-03-19
##### Added
- sparse column support
- model metadata support for hyperparams and data type schema
- release v1.5.2

#### [1.5.1] - 2021-03-09
##### Fixed
- fix/improve data transfer between Py and Java via py4j
- release v1.5.1

#### [1.5.0] - 2021-02-26
##### Added
- install dependencies into an image if there is a requirements.txt file in the code dir
- release v1.5.0

#### [1.4.16] - 2021-02-18
##### Added
- `/info` endpoint
- progress spinner when building a docker images

##### Fixed
- unset entrypoint when running DRUM in docker

#### [1.4.15] - 2021-02-11
##### Fixed
- dataset temp naming for failed validation checks
- command line argument parsing

#### [1.4.14] - 2021-02-08
##### Added
- make DRUM return predictions in DR format when deployment config is provided
##### Changed
- default perf tests timeout from 180 to 600 s
- refactor model metadata YAML schema

#### [1.4.13] - 2021-02-01
##### Added
- custom Java predictors support
##### Changes
- apply --skip-predict if SKIP_PREDICT env var is present
##### Fixed
- don't fail on spaces in binary class labels in prediction checks
- fix error where X has colname '0' and target is unnamed

#### [1.4.12] - 2021-01-19
##### Changes
- bugfix to prevent resampling of data
- surface warning but don't error out if prediction consistency check fails
##### Fixed
- don't fail on spaces in binary class labels in prediction checks

#### [1.4.11] - 2021-01-14
##### Changes
- transform server passes back formats for both transformed X and y
- transform server passes back column names if transformed X is sparse

#### [1.4.10] - 2021-01-11
##### Added
- support providing arguments via env vars, e.g `TARGET_TYPE regression` is the same as `--target-type regression`
##### Changes
- prediction side effects check no longer run for custom transforms; still assert that transform server launches and returns 200 response
- test coverage confirming support of sparse input and output for custom transforms and transform server
##### Removed
-- `--unsupervised` arg support

#### [1.4.9] - 2020-12-29
##### Changes
- `transform` mode now takes and returns both `X` and `y`. The `transform` hook must use both arguments for custom transforms,
 but need only return `X` (if `y` is not returned, it will not be transformed)
- The user may forgo a `transform` hook for custom transforms if they use an sklearn artifact. If the user does not define
`transform`, the target will not be used in transforming the fatures and will remain un-transformed.
- Added support for multiclass to drum push in anticipation of the release of datarobot client v2.22
- check if payload format (csv/mtx/arrow) is supported

#### [1.4.8] - 2020-12-11
##### Fixed
- Force class labels to be strings

#### [1.4.7] - 2020-12-11
##### Added
- do predictions side effects check (when fitting a model)
##### Fixed
- Handling of class mapping to class order with numeric values

#### [1.4.6] - 2020-12-08
##### Added
- **/predictions** and **/predictionsUnstructured** endpoints as aliases for **/predict** and **/predictUnstructured**
- handling the case when input sent as binary data
##### Fixed
- Validation of numeric multiclass class labels should always compare as strings

#### [1.4.5] - 2020-12-02
##### Added
-  **/transform** endpoint added to prediction server 
##### Changes
- Allow multiclass to function with only 2 labels

#### [1.4.4] - 2020-11-24
##### Added
- New `transform` target type for performing pre-/post- processing on features/targets
##### Changes
- Unpin pyarrow version

#### [1.4.3] - 2020-11-17
##### Added
- Compare DRUM version on host and container when running in *--docker* mode
##### Fixed
- Arrow format input data support

#### [1.4.2] - 2020-11-14
##### Added
- Support for a single uwsgi process in production mode
- Capabilities endpoint
- Arrow format input data support

##### Changed
- Change dependency for new major release of mlpiper v2.4.0, which executes RESTful pipeline in a single uWSGI process
- Catch and report exceptions from user's code
- Set Flask server (no production) logging level to the level from the command line

##### Fixed
- Fixed issue with multiclass scoring failing with numerical class labels
- Fixed multiclass class labels file not working in --docker mode

#### [1.4.1] - 2020-10-29
##### Added
- H2O driverless AI mojo pipeline support
- fit on sparse data
- `predictUnstructured` endpoint for uwsgi-based prediction server

#### [1.4.0] - 2020-10-23
##### Added
- `multiclass` target type
- `class-labels` for specifying the class labels of a multiclass model
- `class-labels-file` for specifying a file containing the class labels of a multiclass model
- add multiclass classification support for `drum score` and `drum server`
##### Changed
- support only keras built into tensorflow >= 2.2.1
- `--target-type` is now required for `drum fit`

#### [1.3.0] - 2020-10-15
##### Added
- `read_input_data` hook
- add `target-type` param
- unstructured mode

#### [1.2.0] - 2020-08-28
##### Added
- optional **--language [python|r|java]** argument to enforce execution framework
- uwsgi/nginx powered prediction server
- **-max-workers** argument to limit number of workers in production server mode

##### Removed
- **--threaded** argument from Flask server mode

##### Changed
- dependencies: mlpiper==2.3.0, py4j~=0.10.9
- optional **--unsupervised** argument and handling for unsupervised Fit in python

#### [1.1.4] - 2020-08-04
##### Added
- the docker flag now takes a directory, and will build a docker image
- the `push` verb lets you add your code into DataRobot. 
- H2O models support
- r_lang fit component, pipeline, and template
##### Changed
- search custom.py recursively in the code dir
- set rpy2 dependcy <= 3.2.7 to avoid pandas import error 

## [1.1.3] - 2020-07-17
### Added
- error server is started in case of imports/pipeline failures
- drum_autofit() helper for sklearn estimator
### Changed
- updated Java predictor dependencies

## [1.1.2] - 2020-06-18
### Added
- PMML support

## [1.1.1] - 2020-06-10
### Added
- language detection by artifact and custom.py/R

### Changed
- now version check is called as `drum --version`

## [1.1.0] - 2020-05-29
### Changed
- public envs are pinned to drum==1.1.0

## [1.0.20] - 2020-05-28
### Changed
- the name to **drum**

## [1.0.19] - 2020-05-18
### Changed
- build only Python 3 wheel

## [1.0.18] - 2020-05-12
### Added
- cmrunner for custom model fit
- fit code to python3_sklearn model template

### Fixed
- printing result if `--output` is not provided

## [1.0.17] - 2020-05-07
### Changed
- change predict() hook to score()
- change signature to `score(data, mode, **kwargs)`
- change command `cmrun predict` to `cmrun score`

### Added
- `new` subcommand for model templates creation 

## [1.0.16] - 2020-05-05
### Changed
- unpin rpy2 dependency version

## [1.0.15] - 2020-05-04
### Changed
- require to use sub-command, e.g. `cmrun predict`  

## [1.0.14] - 2020-04-30
### Changed
- refactored command/subcommand usage

## [1.0.13] - 2020-04-27
### Added
- CMRUNNER_JAVA_XMX env var to pass max heap memory value to JVM
- autocompletion support
- performance tests feature

## [1.0.12] - 2020-04-23
### Changed
- optimized py4j usage for java predictor

## [1.0.11] - 2020-04-21
### Changed
- improved class labels handling in R binary classification

## [1.0.10] - 2020-04-20
### Added
- --threaded flag which allows to start cmrunner prediction server(Flask) in threaded mode
### Changes
- replaced custom hooks for R with
    - init() -> NULL
    - load_model(input_dir: character) -> Any
    - transform(data: data.frame, model: Any) -> data.frame
    - predict(data: data.frame, model: Any, positive_class_label: character, negative_class_label: character) -> data.frame
    - post_process(predictions: data.frame, model: Any) -> data.frame
- unify argument names in file reading/writing components

## [1.0.9] - 2020-04-16
### Changes
- improved prediction server response serialization

## [1.0.8] - 2020-04-10
### Added
- support for --docker command line option. Running the model inside a docker image

## [1.0.7] - 2020-04-08
### Added
- support Java Codegen models in batch and server modes

## [1.0.6] - 2020-04-03
### Changed
- replaced custom hooks for python with
    - init() -> None
    - load_model(input_dir: str) -> Any
    - transform(data: DataFrame, model: Any) -> DataFrame
    - predict(data: DataFrame, model: Any, positive_class_label: str, negative_class_label: str) -> DataFrame
    - post_process(predictions: DataFrame, model: Any) -> DataFrame

## [1.0.5] - 2020-03-30
### Added
- handle class labels for scikit-learn and R binary classification

## [1.0.4] - 2020-03-20
### Added
- make rpy2 dependency optional

## [1.0.3] - 2020-03-20
### Added
- R models support

## [1.0.2] - 2020-03-19
### Changed
- Change dep: mlpiper==2.2.0
- Bump version to push to test PyPI

## [1.0.1] - 2020-03-09
### Added
- Added wheelhouse for distributing "mlpiper"
- Added README
