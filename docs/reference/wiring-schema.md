# Wiring Schema

Schema for `control.yaml`, `readout_send.yaml`, and `readout_return.yaml`.

Source: [`schema/wiring.schema.json`](https://github.com/cryo-wiring/spec/blob/main/schema/wiring.schema.json)

## Top-Level Structure

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `modules` | object | No | Reusable module definitions |
| `lines` | array | **Yes** | List of line configurations |

## Module

Each key in `modules` defines a named module.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `stages` | object | **Yes** | Component definitions per stage |

Stage keys must be one of: `RT`, `50K`, `4K`, `Still`, `CP`, `MXC`.

Each stage value is an array of [component references](#component-reference).

```yaml
modules:
  control_standard:
    stages:
      50K:
        - XMA-10dB
      4K:
        - XMA-20dB
```

## Line

Each item in `lines` uses one of two formats:

- **Module reference** — Specifies `module` and optionally `stages` for overrides (`add`/`remove`)
- **Flat (inline)** — Specifies `stages` directly with component lists. `module` must not be present.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `line_id` | string | **Yes** | Line identifier. Pattern: `^(C\|RS\|RR)\d+$` |
| `qubit` | string | No | Associated qubit (for control lines). Pattern: `^Q\d+$` |
| `qubits` | array of string | No | Associated qubits (for readout lines). Each: `^Q\d+$` |
| `module` | string | No | Referenced module name |
| `stages` | object | No | Per-stage components or overrides |

### Variant 1: Module Reference

The line inherits all components from the named module. Optional `stages` can override specific stages.

```yaml
- line_id: C00
  qubit: Q00
  module: control_standard
```

### Variant 2: Flat (Inline Stages)

The line defines all components directly. `module` must not be present.

```yaml
- line_id: C00
  qubit: Q00
  stages:
    4K:
      - type: attenuator
        model: XMA-2082-6431-20
        value_dB: 20
```

## Stage Overrides

When a line references a module, its `stages` object uses `add` / `remove` instead of a component list.

| Property | Type | Description |
|----------|------|-------------|
| `add` | array | Components to append |
| `remove` | array | Components to remove (by key or `{model: "..."}`) |

```yaml
- line_id: C01
  qubit: Q01
  module: control_standard
  stages:
    4K:
      remove:
        - XMA-20dB
      add:
        - XMA-10dB
        - LPF-KL
```

## Component Reference

A component reference is one of:

### String Key

A key name defined in `components.yaml`.

```yaml
- XMA-20dB
```

### Inline Object

A full component definition.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `type` | enum | **Yes** | `attenuator`, `filter`, `isolator`, or `amplifier` |
| `model` | string | **Yes** | Model number |
| `serial` | string | No | Serial number |
| `value_dB` | number | No | Attenuation in dB (attenuator) |
| `gain_dB` | number | No | Gain in dB (amplifier) |
| `filter_type` | string | No | Filter type (e.g., `Eccosorb`) |
| `amplifier_type` | string | No | Amplifier type (e.g., `HEMT`) |

```yaml
- type: amplifier
  model: LNF-LNC4_8C
  amplifier_type: HEMT
  gain_dB: 38
```

## Stage Names

| Value | Description |
|-------|-------------|
| `RT` | Room temperature |
| `50K` | 50 Kelvin |
| `4K` | 4 Kelvin |
| `Still` | Still |
| `CP` | Cold plate |
| `MXC` | Mixing chamber |
