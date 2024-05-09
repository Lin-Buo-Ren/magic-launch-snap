# The `magic-launch` snap enablement launcher

This launcher fixes libmagic file type autodetection compatibility in snaps.

Refer [the Snapcraft Forum topic](https://forum.snapcraft.io/t/the-magic-launch-launcher-fix-file-type-detection-based-on-libmagic/10442) for more info regarding the use of this stage snap.

<https://gitlab.com/brlin/magic-launch>  
[![The GitLab CI pipeline status badge of the project's `main` branch](https://gitlab.com/brlin/magic-launch/badges/main/pipeline.svg?ignore_skipped=true "Click here to check out the comprehensive status of the GitLab CI pipelines")](https://gitlab.com/brlin/magic-launch/-/pipelines) [![GitHub Actions workflow status badge](https://github.com/brlin-tw/magic-launch/actions/workflows/check-potential-problems.yml/badge.svg "GitHub Actions workflow status")](https://github.com/brlin-tw/magic-launch/actions/workflows/check-potential-problems.yml) [![pre-commit enabled badge](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white "This project uses pre-commit to check potential problems")](https://pre-commit.com/) [![REUSE Specification compliance badge](https://api.reuse.software/badge/gitlab.com/brlin/magic-launch "This project complies to the REUSE specification to decrease software licensing costs")](https://api.reuse.software/info/gitlab.com/brlin/magic-launch)

## How to use

1. Merge the following part definition to your Snapcraft recipe:

    ```yaml
    parts:
      # Launcher for fixing libmagic applications
      # https://forum.snapcraft.io/t/the-magic-launch-launcher-fix-file-type-detection-based-on-libmagic-in-the-snap-runtime/10442
      magic-launch:
        source: https://gitlab.com/brlin/magic-launch.git
        source-tag: v2.0.3
        plugin: dump
        stage:
          - bin/*
    ```

1. In the `apps` stanza, insert `bin/magic-launch` into the command chain:

   ```yaml
   apps:
     _app_name_:
       # The command to run the application, the value should be a
       # *relative path* to an executable file rooted from the `prime` directory
       command: bin/magic-launch "${SNAP}"/bin/_app_command_
   ```

   if you're using the `full` adapter:

   ```yaml
   apps:
     _app_name_:
       # The environment adapter style to use, `command-chain` is only supported
       # by the `full` adapter
       adapter: full

       # The command to run the application, the value should be a
       # *relative path* to an executable file rooted from the `prime` directory
       command: bin/_app_command_
       command-chain:
         - bin/magic-launch
   ```

## Snaps that use this launcher

* [Install (UNOFFICIAL) nano for Linux using the Snap Store | Snapcraft](https://snapcraft.io/nano) - [source](https://github.com/snapcrafters/nano)

## Reference

The following materials are referenced during the development of this product:

* The file(1) manual page
* The magic(5) manual page

## Licensing

Unless otherwise noted(individual file's header/[REUSE DEP5](.reuse/dep5)), this product is licensed under [the MIT license](https://opensource.org/license/MIT), or any of its recent versions you would prefer.

This work complies to [the REUSE Specification](https://reuse.software/spec/), refer the [REUSE - Make licensing easy for everyone](https://reuse.software/) website for info regarding the licensing of this product.
