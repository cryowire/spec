# Component Types

## Overview

Components are RF/microwave parts installed at specific temperature stages along the wiring path.

All components share these common fields:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `type` | string | Yes | Component type |
| `model` | string | Yes | Model number |
| `serial` | string | No | Serial number |

## Types

### Attenuator

Reduces signal power by a fixed amount.

| Field | Type | Description |
|-------|------|-------------|
| `value_dB` | number | Attenuation in dB |

```yaml
type: attenuator
model: XMA-2082-6431-20
value_dB: 20
```

### Filter

Passes or blocks specific frequency ranges.

| Field | Type | Description |
|-------|------|-------------|
| `filter_type` | string | Filter type (e.g., `Lowpass`, `Eccosorb`) |

```yaml
type: filter
model: KL-Lowpass-12G
filter_type: Lowpass
```

### Isolator

Allows signal to pass in one direction only. No type-specific fields.

```yaml
type: isolator
model: QCI-CIC4-12
```

### Amplifier

Increases signal power.

| Field | Type | Description |
|-------|------|-------------|
| `amplifier_type` | string | Amplifier type (e.g., `HEMT`, `RT`) |
| `gain_dB` | number | Gain in dB |

```yaml
type: amplifier
model: LNF-LNC4_8C
amplifier_type: HEMT
gain_dB: 38
```

## Component Catalog

Components can be defined in a `components.yaml` catalog and referenced by key name:

```yaml
# components.yaml
XMA-20dB:
  type: attenuator
  model: XMA-2082-6431-20
  value_dB: 20

LNF-HEMT:
  type: amplifier
  model: LNF-LNC4_8C
  amplifier_type: HEMT
  gain_dB: 38
```

These keys can then be used directly in wiring configurations instead of inline definitions.
