# LingmoOS Manifest

This repository contains the Repo manifest definitions for the LingmoOS source tree.

It manages source repositories, synchronization configurations, and different source code configurations for LingmoOS.

## Repository Structure

```text
manifest/
├── default.xml
├── manifests/
│   ├── standard.xml
│   └── universe.xml
└── projects/
    ├── graphics.xml
    ├── kernel.xml
    └── lingmo.xml
```

### Manifests

The `manifests/` directory contains different source configurations.

| Manifest | Description |
|---|---|
| `default.xml` | Default manifest entry point |
| `standard.xml` | Standard LingmoOS source configuration |
| `universe.xml` | Complete source configuration, including additional upstream projects |

### Projects

The `projects/` directory contains reusable project definitions.

| File | Description |
|---|---|
| `lingmo.xml` | LingmoOS projects and components |
| `graphics.xml` | Graphics-related upstream projects |
| `kernel.xml` | Linux kernel and related projects |

## Getting Started

Install [Repo](https://gerrit.googlesource.com/git-repo/) first.

Initialize the source tree using one of the following configurations.

### Standard

```bash
repo init -u https://github.com/LingmoOS/manifest.git \
    -m manifests/standard.xml
repo sync
```

### Universe

```bash
repo init -u https://github.com/LingmoOS/manifest.git \
    -m manifests/universe.xml
repo sync
```

## Source Synchronization

Synchronize all configured projects:

```bash
repo sync
```

Synchronize with parallel jobs:

```bash
repo sync -j8
```

## Contributing

Please keep manifest definitions organized and consistent.

- Add LingmoOS-maintained repositories to `projects/lingmo.xml`.
- Add upstream graphics dependencies to `projects/graphics.xml`.
- Add kernel-related repositories to `projects/kernel.xml`.
- Add new source configurations under `manifests/`.

## License

The manifest definitions in this repository are provided under the repository's applicable license. Individual projects retain their respective licenses.
