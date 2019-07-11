# Archived

This repository is not being actively maintained, and has been archived.

# renovate-config

[![CircleCI](https://circleci.com/gh/factset/renovate-config.svg?style=svg)](https://circleci.com/gh/factset/renovate-config)

> Common Renovate configuration for FactSet's official standards and best practices.

Common configuration for customizing the behavior of the [Renovate App](https://github.com/marketplace/renovate) for a project.

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Installation](#installation)
- [Usage](#usage)
  - [Default Preset](#default-preset)
    - [Features](#features)
  - [Web Preset](#web-preset)
    - [Features](#features-1)
  - [Python Preset](#python-preset)
  - [Multiple Presets Together](#multiple-presets-together)
- [Contributing](#contributing)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Installation

No installation is necessary to use this configuration package for Renovate.

## Usage

To configure Renovate for your repository, copy and paste the `extends` line for your preferred configuration into a supported [_Configuration location_](https://renovateapp.com/docs/getting-started/configure-renovate#configuration-location).

While our `default` configuration enables many useful Renovate features, we strongly recommend you select one of our language-specific configurations.

### Default Preset

Configuration common to all development communities at FactSet.

```json
{
  "extends": ["@fds"]
}
```

`"@fds"` is based on Renovate's `default` configuration with a few changes listed in the _Features_ section below.

#### Features

**Group Docker Digest Updates**

All [Docker digest updates](https://renovateapp.com/docs/language-support/docker#digest-updating) in a project that need to be updated will be grouped into a single Renovate pull request, and if status checks pass, the pull request is automatically merged.

Grouping digest updates allows us to reduce the number of notifications sent to project maintainers. Often an update to a low-level Docker image, such as Alpine, will lead to many downstream Docker images, such as [Node images](https://hub.docker.com/_/node/) being rebuilt. When that happens, each reference to a Node docker image in a repository will have its digest updated, and if grouping is not enabled, each digest update would be in a separate pull request.

### Web Preset

Configuration that adheres to the Web Guidance Group standards.

```json
{
  "extends": ["@fds:web"]
}
```

> **Note:** Extends the `default` configuration.

#### Features

**Lockfile Maintenance**

All FactSet projects will receive a regularly scheduled pull request to update the contents of the project's lockfile (whether `package-lock.json` or `yarn.lock`).

We schedule regular lockfile updates to ensure projects are using the latest [Semantic Version](https://semver.org/) compatible releases of their dependencies.

FactSet, along with our clients, benefit if all our products are routinely updated to use the latest [Semantic Version](https://semver.org/) compatible releases.

Our clients benefit from a consistent experience across FactSet products when a bug has been fixed in a shared library and every product at FactSet has been updated to use that patch.

FactSet benefits in the same scenario because a single bug fix will be deployed across all products automatically so that clients aren't encountering, and then reporting, the same issue against multiple products. That saves FactSet resources triaging those reports, and avoids our reputation being tarnished by a single bug effecting a single client multiple times.

To smooth the adoption of regular lockfile updates, and lower the costs associated with manually accepting lockfile maintenance pull requests every week, all lockfile maintenance pull requests are merged automatically if all [Status Checks](https://blog.github.com/2014-12-08-see-results-from-all-pull-request-status-checks/) pass.

**Angular Dependency Updates**

All npm packages that must be updated in lock-step with `angular`, and `angualr` itself, will be bundled into a single pull request, and those dependencies will only be updated to conform to our _JavaScript Application Framework Standard_.

**TypeScript Dependency Updates**

All npm packages that must be updated in lock-step with `typescript`, and `typescript` itself, will be bundled into a single pull request, and those dependencies will only be updated to conform to our _Web Programming Language Standard_.

### Python Preset

Configuration that adheres to best practices within the Python community at FactSet.

```json
{
  "extends": ["@fds:python"]
}
```

> **Note:** Extends the `default` configuration.

### Multiple Presets Together

If you wish to combine two or more of our language-specific presets, you can provide all desired presets as an array to the `extends` property.

```json
{
  "extends": ["@fds:web", "@fds:python"]
}
```

In this example, if any options conflict between the `@fds:web` or `@fds:python` presets, the options in the last preset listed will take precedence.

## Contributing

Please check out our [contributing guide](https://github.com/factset/renovate-config/blob/master/CONTRIBUTING.md) to see how you may contribute to this project.

## Copyright

Copyright 2018 FactSet Research Systems Inc

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
