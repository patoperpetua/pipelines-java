# SINGLETON SD - PIPELINES - JAVA

This project contains JAVA gitlab-ci templates.

> The **main repository** is hosted in [gitlab.com/singletonsd/pipelines/java](https://gitlab.com/singletonsd/pipelines/java.git) but it is automatically mirrored to [github.com/singletonsd](https://github.com/singletonsd/pipelines-java.git), [github.com/patoperpetua](https://github.com/patoperpetua/pipelines-java.git) and to [gitlab.com/patoperpetua](https://gitlab.com/patoperpetua/pipelines-java.git). If you are in the Github page it may occur that is not updated to the last version.

## AVAILABLE FILES

There is 1 file:

- **main:** contains jobs to compile, test, package and deploy a java maven project. If there is a settings file in the project, it will use it in every job. There is 4 jobs:
  - **build:** build project. It does not have variables.
  - **test:** test the project only if *JAVA_MAIN_EXECUTE_TEST* is defined. It has the following available variables:
    - *JAVA_MAIN_EXECUTE_TEST:* "true"
  - **package:** create a jar file. It does not have variables.
  - **deploy:** publish the project to a defined maven project only if *JAVA_MAIN_EXECUTE_DEPLOY* is defined and the repository name is the same as defined in *ORIGINAL_REPOSITORY* variable. It has the following available variables:
    - *JAVA_MAIN_EXECUTE_DEPLOY:* "true"

## HOW TO

### USE

If you want to skip reading, you can copy and paste one of the following links and setup the variables:

- [Main](https://gitlab.com/singletonsd/pipelines/java/raw/master/examples/.gitlab-ci-main.yml)

To use it, you can include them as following (using repository aproach):

```yaml
include:
  - project: 'singletonsd/pipelines/java'
    file: '/src/.gitlab-ci-main.yml'
```

Or using remote approach over gitlab repo:

```yaml
include:
  - remote: 'https://gitlab.com/singletonsd/pipelines/java/raw/master/src/.gitlab-ci-main.yml'
```

Or using remote approach over gitlab pages:

```yaml
include:
  - remote: 'https://singletonsd.gitlab.io/pipelines/java/latest/.gitlab-ci-main.yml'
```

Master branch is setup as latest folder. To use an specific version, put the version name before the file name like:

```yaml
include:
  - remote: 'https://singletonsd.gitlab.io/pipelines/java/1.0.0/.gitlab-ci-${FILE}.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/java/develop/.gitlab-ci-${FILE}.yml'
  - remote: 'https://singletonsd.gitlab.io/singletonsd/pipelines/java/feature-new/.gitlab-ci-test-${FILE}.yml'
```

And also define the stages you want to use, like following:

```yaml
# Main
stages:
  - build
  - test
  - deploy
  - package
```

### TEST

You can test your .gitlab-ci.yml files by executing the following:

```bash
curl -s https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_test_standalone.sh | bash /dev/stdin
```

That script contains the following options:

```bash
-h | --help: display help.
-o | --only: the name of the file or folder to test.
```

Also you can download the script by:

```bash
curl -o gitlab-ci_lint_test_standalone.sh -L https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_test_standalone.sh
```

## GIT HOOK

You can setup gitlab lint tester to be run before a commit. To do that just execute the following script under your git repository:

```bash
curl -s https://singletonsd.gitlab.io/scripts/gitlab-ci/latest/gitlab-ci_lint_hook_installer.sh | bash /dev/stdin
```

## DOCUMENTATION

- [Gitlab CI - Includes](https://docs.gitlab.com/ee/ci/yaml/)

## TODO

- [X] Add main template.
- [X] Fix documentation.
- [X] Add examples.

----------------------

© [Singleton SD](http://www.singletonsd.com), Italy, 2019.
