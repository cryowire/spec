# cryo-wiring-spec

Specification for dilution refrigerator wiring configuration data.

## Overview

This repository defines the YAML data format specification used across the cryo-wiring ecosystem.

- [cryo-wiring-cli](https://github.com/cryo-wiring/cli) — Core library + CLI (reference implementation of this spec)
- [cryo-wiring-app](https://github.com/cryo-wiring/app) — Web UI
- [cryo-wiring-template](https://github.com/cryo-wiring/template) — Data repository template

## Examples

See the [`examples/`](examples/) directory for complete sample files:

| File | Description |
|------|-------------|
| [`components.yaml`](examples/components.yaml) | Component catalog |
| [`metadata.yaml`](examples/metadata.yaml) | Cooldown metadata |
| [`control.yaml`](examples/control.yaml) | Control wiring (module format) |
| [`readout_send.yaml`](examples/readout_send.yaml) | Readout send wiring (module format) |
| [`readout_return.yaml`](examples/readout_return.yaml) | Readout return wiring (flat format) |

## Schema

| File | Description |
|------|-------------|
| `schema/wiring.schema.json` | Wiring configuration (control.yaml, readout_send.yaml, readout_return.yaml) |
| `schema/metadata.schema.json` | Cooldown metadata (metadata.yaml) |

## Directory Structure

Data repositories follow this structure:

```text
my-fridge-data/
├── components.yaml              # Component catalog
├── templates/
│   ├── control_module.yaml      # Control line module template
│   ├── readout_send_module.yaml # Readout send line module template
│   └── readout_return_module.yaml # Readout return line module template
├── <fridge-name>/
│   ├── chip.yaml                # Chip information
│   ├── current/                 # Working cooldown
│   │   ├── metadata.yaml
│   │   ├── control.yaml
│   │   ├── readout_send.yaml
│   │   └── readout_return.yaml
│   └── <YYYY-NNN>/             # Snapshot
│       ├── metadata.yaml
│       ├── control.yaml
│       ├── readout_send.yaml
│       └── readout_return.yaml
```

## Temperature Stages

Wiring is organized across 6 temperature stages:

| Stage | Temperature |
|-------|-------------|
| `RT` | Room temperature |
| `50K` | 50 Kelvin |
| `4K` | 4 Kelvin |
| `Still` | Still |
| `CP` | Cold plate |
| `MXC` | Mixing chamber |

## Component Types

| Type | Description | Specific Fields |
|------|-------------|-----------------|
| `attenuator` | Attenuator | `value_dB` (attenuation) |
| `filter` | Filter | `filter_type` (e.g., Lowpass, Eccosorb) |
| `isolator` | Isolator | — |
| `amplifier` | Amplifier | `amplifier_type` (e.g., HEMT, RT), `gain_dB` (gain) |

Common fields for all components: `type`, `model`, `serial` (optional)

## Line Configuration

### Line Types

| Type | Prefix | Identifier | Description |
|------|--------|------------|-------------|
| Control | `C` | `qubit` (single) | Input line for qubit control signals |
| Readout Send | `RS` | `qubits` (multiple) | Input line for readout signals (4-multiplexed) |
| Readout Return | `RR` | `qubits` (multiple) | Output line for readout signals (4-multiplexed) |

### Module Format

Lines can reference modules. Per-stage overrides are supported via `add` / `remove`.

```yaml
modules:
  control_standard:
    stages:
      50K:
      - XMA-10dB
      4K:
      - XMA-20dB
      MXC:
      - XMA-20dB

lines:
- line_id: C00
  qubit: Q00
  module: control_standard
- line_id: C01
  qubit: Q01
  module: control_standard
  stages:
    4K:
      add:
      - LPF-KL
```

### Flat Format

Components can also be specified directly on each line without using modules.

```yaml
lines:
- line_id: C00
  qubit: Q00
  stages:
    50K:
    - type: attenuator
      model: XMA-2082-6431-10
      value_dB: 10
    4K:
    - type: attenuator
      model: XMA-2082-6431-20
      value_dB: 20
```
