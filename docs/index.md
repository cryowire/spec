# Cryo Wiring Specification

Specification for dilution refrigerator wiring configuration data in YAML format.

## About This Spec

cryowire-spec defines a YAML data format for describing RF/microwave wiring configurations inside dilution refrigerators.
It standardizes wiring configuration management so that the [cryowire/cli](https://github.com/cryowire/cli) and [cryowire/app](https://github.com/cryowire/app) can work with the data in a consistent way.

## Specification Contents

### Guide

Step-by-step explanation of each element of the spec.

| Section                                             | Description                                                     |
| --------------------------------------------------- | --------------------------------------------------------------- |
| [Directory Structure](guide/directory-structure.md) | File layout and roles in a data repository                      |
| [Temperature Stages](guide/temperature-stages.md)   | The 6 temperature stages from RT to MXC and signal direction    |
| [Component Types](guide/component-types.md)         | Attenuator, filter, isolator, and amplifier definitions         |
| [Line Configuration](guide/line-configuration.md)   | Control / Readout Send / Readout Return lines and module format |
| [Examples](guide/examples.md)                       | Complete YAML sample files                                      |

### Schema Reference

Exhaustive field-level definitions for each YAML file.

| Section | Target Files |
|---------|-------------|
| [Wiring Schema](reference/wiring-schema.md) | `control.yaml` / `readout_send.yaml` / `readout_return.yaml` |
| [Components Schema](reference/components-schema.md) | `components.yaml` |
| [Metadata Schema](reference/metadata-schema.md) | `metadata.yaml` |
| [Chip Schema](reference/chip-schema.md) | `chip.yaml` |

## Quick Start

Data repositories follow this structure:

```text
my-cryo-data/
├── components.yaml              # Component catalog
├── templates/                   # Module templates
│   ├── control_module.yaml
│   ├── readout_send_module.yaml
│   └── readout_return_module.yaml
├── <cryo-name>/
│   └── <YYYY>/                  # Year group
│       ├── cd001/               # Cooldown directory
│       │   ├── metadata.yaml
│       │   ├── chip.yaml
│       │   ├── control.yaml
│       │   ├── readout_send.yaml
│       │   ├── readout_return.yaml
│       │   └── cooldown.yaml    # Resolved bundle
│       └── cd002/
│           └── ...
```

Use [cryowire/template](https://github.com/cryowire/template) to get started quickly.

See **[cryowire.github.io](https://cryowire.github.io/)** for the full project overview.
