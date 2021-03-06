# rootless-docker

[![GitHub Action: Try Me](https://img.shields.io/badge/GitHub_Action-Try_Me-FF6978?logo=githubactions&logoColor=2088FF)](https://github.com/marketplace/actions/rootless-docker)
[![Rootless Docker](https://img.shields.io/badge/Docker-Rootless-FF5666?logo=docker&logoColor=2496ED)](https://docs.docker.com/engine/security/rootless/)
[![Test Workflow Status](https://github.com/ScribeMD/rootless-docker/workflows/Test/badge.svg)](https://github.com/ScribeMD/rootless-docker/actions/workflows/test.yaml)
[![Copy/Paste: 0%](https://img.shields.io/badge/Copy%2FPaste-0%25-B200B2?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik03LjAyNCAzLjc1YzAtLjk2Ni43ODQtMS43NSAxLjc1LTEuNzVIMjAuMjVjLjk2NiAwIDEuNzUuNzg0IDEuNzUgMS43NXYxMS40OThhMS43NSAxLjc1IDAgMDEtMS43NSAxLjc1SDguNzc0YTEuNzUgMS43NSAwIDAxLTEuNzUtMS43NVYzLjc1em0xLjc1LS4yNWEuMjUuMjUgMCAwMC0uMjUuMjV2MTEuNDk4YzAgLjEzOS4xMTIuMjUuMjUuMjVIMjAuMjVhLjI1LjI1IDAgMDAuMjUtLjI1VjMuNzVhLjI1LjI1IDAgMDAtLjI1LS4yNUg4Ljc3NHoiLz48cGF0aCBkPSJNMS45OTUgMTAuNzQ5YTEuNzUgMS43NSAwIDAxMS43NS0xLjc1MUg1LjI1YS43NS43NSAwIDExMCAxLjVIMy43NDVhLjI1LjI1IDAgMDAtLjI1LjI1TDMuNSAyMC4yNWMwIC4xMzguMTExLjI1LjI1LjI1aDkuNWEuMjUuMjUgMCAwMC4yNS0uMjV2LTEuNTFhLjc1Ljc1IDAgMTExLjUgMHYxLjUxQTEuNzUgMS43NSAwIDAxMTMuMjUgMjJoLTkuNUExLjc1IDEuNzUgMCAwMTIgMjAuMjVsLS4wMDUtOS41MDF6Ii8+PC9zdmc+)](https://github.com/kucherenko/jscpd)

[![Automated Updates: Dependabot](https://img.shields.io/badge/Dependabot-Automated_Updates-C98686?logo=dependabot&logoColor=025E8C)](https://github.com/dependabot)
[![Package Management: Poetry](https://img.shields.io/badge/Poetry-Package_Management-F58A07?logo=poetry&logoColor=60A5FA)](https://python-poetry.org/)
[![Git Hooks: pre-commit](https://img.shields.io/badge/pre--commit-Git_Hooks-66A182?logo=precommit&logoColor=FAB040)](https://pre-commit.com/)
[![Commit Style: Conventional Commits](https://img.shields.io/badge/Conventional_Commits-Commit_Style-F39237?logo=conventionalcommits&logoColor=FE5196)](https://conventionalcommits.org)
[![Releases: Semantic Versioning](https://img.shields.io/badge/SemVer-Releases-40C9A2?logo=semver&logoColor=3F4551)](https://semver.org/)
[![Code Style: Prettier](https://img.shields.io/badge/Prettier-Code_Style-758ECD?logo=prettier&logoColor=F7B93E)](https://prettier.io/)
[![Code Style: EditorConfig](https://img.shields.io/badge/EditorConfig-Code_Style-CF995F?logo=editorconfig&logoColor=FEFEFE)](https://editorconfig.org/)
[![Editor: Visual Studio Code](https://img.shields.io/badge/VSCode-Editor-E54B4B?logo=visualstudiocode&logoColor=007ACC)](https://code.visualstudio.com/)

Run Docker in Rootless Mode to Prevent Permission Errors

<!--TOC-->

- [rootless-docker](#rootless-docker)
  - [Usage](#usage)
  - [Supported Runners](#supported-runners)
  - [Permissions](#permissions)
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
    uses: ScribeMD/rootless-docker@0.1.7
  ```

## Supported Runners

- Tested on `ubuntu-20.04`
- Probably works on `ubuntu-18.04`
- May work on future versions of Linux
- Definitely doesn't work on Windows or macOS since Docker only offers rootless
  mode on Linux

## Permissions

No
[permissions](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token)
are required.

## Changelog

Please refer to [`CHANGELOG.md`](CHANGELOG.md).
