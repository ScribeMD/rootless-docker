# rootless-docker

[![Test](https://github.com/ScribeMD/rootless-docker/workflows/Test/badge.svg)](https://github.com/ScribeMD/rootless-docker/actions/workflows/test.yaml)
[![Bump Version](https://github.com/ScribeMD/rootless-docker/workflows/Bump%20Version/badge.svg)](https://github.com/ScribeMD/rootless-docker/actions/workflows/bump-version.yaml)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg?style=flat-square)](https://conventionalcommits.org)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

Run Docker in Rootless Mode to Prevent Permission Errors

<!--TOC-->

- [rootless-docker](#rootless-docker)
  - [Usage](#usage)
  - [Supported Runners](#supported-runners)
  - [Contributing](#contributing)
  - [Changelog](#changelog)

<!--TOC-->

GitHub-hosted (and many self-hosted) runners use rootful Docker, but the runner
itself does not run as root. As described in
[actions/runner#434](https://github.com/actions/runner/issues/434), files
created by Docker containers are hence owned by root, resulting in permission
errors when the runner attempts to clean up checked out repositories. This
action efficiently prevents those permission errors by running Docker in
rootless mode so that all files are owned by the runner user. This approach has
many benefits as it is:

- safer than elevating the runner to root
- less brittle than changing the ownership/permissions of or deleting files
- simpler than other ways of running rootless Docker
- and fast (~15 seconds on GitHub-hosted runner `ubuntu-20.04`)

[Docker's documentation](https://docs.docker.com/engine/security/rootless/)
discusses rootless mode in detail. If you are running a supported Linux
distribution locally, you can follow the steps there to use rootless mode. If
you aren't sure, you can ask Docker whether it is in rootless mode:

```sh
docker info --format "{{ .ClientInfo.Context }}"
```

## Usage

- Add the following step before your first use of Docker:

```yaml
- name: Use Docker in rootless mode.
  uses: ScribeMD/rootless-docker@0.1.2
```

## Supported Runners

- Tested on `ubuntu-20.04`
- Probably works on `ubuntu-18.04`
- May work on future versions of Linux
- Definitely doesn't work on Windows or macOS since Docker only offers rootless
  mode on Linux

## Contributing

Please refer to [CONTRIBUTING.md](CONTRIBUTING.md).

## Changelog

Please refer to [CHANGELOG.md](CHANGELOG.md).
