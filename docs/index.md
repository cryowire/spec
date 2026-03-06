# cryo-wiring-spec

Specification for dilution refrigerator wiring configuration data in YAML format.

## About This Spec

cryo-wiring-spec defines a YAML data format for describing RF/microwave wiring configurations inside dilution refrigerators.
It standardizes wiring configuration management so that the [CLI tool](https://github.com/cryo-wiring/cli) and [Web UI](https://github.com/cryo-wiring/app) can work with the data in a consistent way.

## Specification Contents

### Guide

Step-by-step explanation of each element of the spec.

| Section | Description |
|---------|-------------|
| [Directory Structure](guide/directory-structure.md) | File layout and roles in a data repository |
| [Temperature Stages](guide/temperature-stages.md) | The 6 temperature stages from RT to MXC and signal direction |
| [Component Types](guide/component-types.md) | Attenuator, filter, isolator, and amplifier definitions |
| [Line Configuration](guide/line-configuration.md) | Control / Readout Send / Readout Return lines and module format |
| [Examples](guide/examples.md) | Complete YAML sample files |

### Schema Reference

Exhaustive field-level definitions for each YAML file.

| Section | Target Files |
|---------|-------------|
| [Wiring Schema](reference/wiring-schema.md) | `control.yaml` / `readout_send.yaml` / `readout_return.yaml` |
| [Metadata Schema](reference/metadata-schema.md) | `metadata.yaml` |

## Quick Start

Data repositories follow this structure:

```text
my-fridge-data/
├── components.yaml              # Component catalog
├── templates/                   # Module templates
│   ├── control_module.yaml
│   ├── readout_send_module.yaml
│   └── readout_return_module.yaml
├── <fridge-name>/
│   ├── chip.yaml                # Chip information
│   ├── current/                 # Working cooldown
│   │   ├── metadata.yaml
│   │   ├── control.yaml
│   │   ├── readout_send.yaml
│   │   └── readout_return.yaml
│   └── <YYYY-NNN>/             # Snapshot
│       └── ...
```

Use [cryo-wiring-template](https://github.com/cryo-wiring/template) to get started quickly.

## Related Repositories

- [cryo-wiring-cli](https://github.com/cryo-wiring/cli) — Core library + CLI (reference implementation of this spec)
- [cryo-wiring-app](https://github.com/cryo-wiring/app) — Web UI
- [cryo-wiring-template](https://github.com/cryo-wiring/template) — Data repository template
