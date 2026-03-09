<p align="center"><a href="https://github.com/cryowire">
  <img src="https://raw.githubusercontent.com/cryowire/artwork/main/logo-type/logotype.png" alt="cryowire" width="600" />
</a></p>

<h1 align="center">cryowire/spec</h1>
<p align="center">Specification for dilution refrigerator wiring configuration data in YAML format.</p>
<p align="center">
  <a href="https://cryowire.github.io/"><img src="https://img.shields.io/badge/Website-cryowire.github.io-38bdf8?style=for-the-badge" alt="Website" /></a>
  <a href="https://cryowire.github.io/spec/"><img src="https://img.shields.io/badge/Docs-Specification-818cf8?style=for-the-badge" alt="Specification" /></a>
</p>

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
