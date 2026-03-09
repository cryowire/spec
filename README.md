# Cryo Wiring Specification

Specification for dilution refrigerator wiring configuration data in YAML format.

**[Read the full specification](https://cryowire.github.io/spec/)**

## Related Repositories

| Repository                                                      | Description                                                |
| --------------------------------------------------------------- | ---------------------------------------------------------- |
| [cryowire/cli](https://github.com/cryowire/cli)           | Core library + CLI (reference implementation of this spec) |
| [cryowire/app](https://github.com/cryowire/app)           | Web UI                                                     |
| [cryowire/template](https://github.com/cryowire/template) | Data repository template                                   |

## Spec Overview

This spec defines a YAML data format for describing RF/microwave wiring configurations inside dilution refrigerators.

- **6 temperature stages** — Component placement from RT (300K) down to MXC (10mK)
- **4 component types** — Attenuator, filter, isolator, amplifier
- **3 line types** — Control, Readout Send, Readout Return
- **Module / flat format** — Supports both reusable module definitions and inline definitions

See the [documentation site](https://cryowire.github.io/spec/) for details.

## Schema

| File                                                      | Description                                                    |
| --------------------------------------------------------- | -------------------------------------------------------------- |
| [`wiring.schema.json`](schema/wiring.schema.json)         | Wiring configuration (control / readout_send / readout_return) |
| [`components.schema.json`](schema/components.schema.json) | Component catalog                                              |
| [`metadata.schema.json`](schema/metadata.schema.json)     | Cooldown metadata                                              |
| [`chip.schema.json`](schema/chip.schema.json)             | Chip information                                               |

## Examples

See the [`examples/`](examples/) directory for complete sample files:

| File                                                  | Description                         |
| ----------------------------------------------------- | ----------------------------------- |
| [`components.yaml`](examples/components.yaml)         | Component catalog                   |
| [`chip.yaml`](examples/chip.yaml)                     | Chip information                    |
| [`metadata.yaml`](examples/metadata.yaml)             | Cooldown metadata                   |
| [`control.yaml`](examples/control.yaml)               | Control wiring (module format)      |
| [`readout_send.yaml`](examples/readout_send.yaml)     | Readout send wiring (module format) |
| [`readout_return.yaml`](examples/readout_return.yaml) | Readout return wiring (flat format) |

## Building Docs Locally

```bash
uv sync --group docs
uv run zensical build
```
