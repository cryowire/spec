# Components Schema

Schema for `components.yaml`.

Source: [`schema/components.schema.json`](https://github.com/cryowire/spec/blob/main/schema/components.schema.json)

## Structure

The file is a mapping of component keys to component definitions. Each key becomes a reusable reference that can be used in wiring configurations.

Additional properties on each component are **not allowed**.

## Component Definition

Each component must specify `type`, `manufacturer`, and `model`. Additional fields depend on the component type.

### Attenuator

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `type` | `"attenuator"` | **Yes** | Component type |
| `manufacturer` | string | **Yes** | Manufacturer name |
| `model` | string | **Yes** | Model number |
| `serial` | string | No | Serial number |
| `value_dB` | number | No | Attenuation in dB |

### Filter

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `type` | `"filter"` | **Yes** | Component type |
| `manufacturer` | string | **Yes** | Manufacturer name |
| `model` | string | **Yes** | Model number |
| `serial` | string | No | Serial number |
| `filter_type` | string | No | Filter type (e.g., `Lowpass`, `Eccosorb`) |

### Isolator

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `type` | `"isolator"` | **Yes** | Component type |
| `manufacturer` | string | **Yes** | Manufacturer name |
| `model` | string | **Yes** | Model number |
| `serial` | string | No | Serial number |

### Amplifier

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `type` | `"amplifier"` | **Yes** | Component type |
| `manufacturer` | string | **Yes** | Manufacturer name |
| `model` | string | **Yes** | Model number |
| `serial` | string | No | Serial number |
| `amplifier_type` | string | No | Amplifier type (e.g., `HEMT`, `RT`) |
| `gain_dB` | number | No | Gain in dB |

## Example

```yaml
--8<-- "examples/components.yaml"
```
