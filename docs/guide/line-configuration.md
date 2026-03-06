# Line Configuration

## Line Types

| Type | Prefix | Identifier | Description |
|------|--------|------------|-------------|
| Control | `C` | `qubit` (single) | Input line for qubit control signals |
| Readout Send | `RS` | `qubits` (multiple) | Input line for readout signals (4-multiplexed) |
| Readout Return | `RR` | `qubits` (multiple) | Output line for readout signals (4-multiplexed) |

- **Control lines** have a 1:1 mapping to qubits (e.g., `C00` controls `Q00`)
- **Readout lines** are 4-multiplexed (e.g., `RS00` serves `Q00`-`Q03`)

## Module Format

Lines can reference a named module that defines the default components at each stage. Per-stage overrides are supported via `add` and `remove`.

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

In this example, `C01` inherits everything from `control_standard` but adds an extra filter at the `4K` stage.

### Override Operations

| Operation | Description |
|-----------|-------------|
| `add` | Append components to the module's stage list |
| `remove` | Remove components by key or model number |

```yaml
stages:
  4K:
    remove:
      - XMA-20dB        # remove by component key
    add:
      - XMA-10dB
      - LPF-KL
```

## Flat Format

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

A line must use either a module reference **or** inline stages — not both simultaneously (though module lines can have override stages).

## Component References

Within stage lists, components can be specified as:

1. **String key** — References a component defined in `components.yaml`
2. **Inline object** — Full component definition with `type`, `model`, and type-specific fields
