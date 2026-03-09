# Chip Schema

Schema for `chip.yaml`.

Source: [`schema/chip.schema.json`](https://github.com/cryowire/spec/blob/main/schema/chip.schema.json)

## Structure

Additional properties are **not allowed**.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `name` | string | **Yes** | Chip name |
| `num_qubits` | integer | **Yes** | Number of qubits on the chip (minimum: 1) |
| `qubits_per_readout_line` | integer | No | Number of qubits multiplexed per readout line (minimum: 1, default: 4) |

## Example

```yaml
--8<-- "examples/chip.yaml"
```
