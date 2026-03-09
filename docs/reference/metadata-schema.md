# Metadata Schema

Schema for `metadata.yaml`.

Source: [`schema/metadata.schema.json`](https://github.com/cryowire/spec/blob/main/schema/metadata.schema.json)

## Structure

Additional properties are **not allowed**.

| Property | Type | Required | Pattern | Description |
|----------|------|----------|---------|-------------|
| `cooldown_id` | string | **Yes** | `^cd\d{3,}$` | Cooldown identifier (e.g., `cd001`) |
| `date` | string | **Yes** | ISO 8601 date | Cooldown date (`YYYY-MM-DD`) |
| `cryo` | string | **Yes** | — | Cryostat name |
| `operator` | string | No | — | Operator name |
| `purpose` | string | No | — | Purpose of the cooldown |
| `notes` | string | No | — | Notes |

## Example

```yaml
cooldown_id: cd001
date: 2026-03-01
cryo: BlueFors-LD400
operator: Alice
purpose: Qubit characterization run
notes: Replaced attenuator on C03 at 4K stage.
```

## Cooldown ID

The `cooldown_id` uses the format `cdNNN` where `NNN` is a zero-padded number of 3 or more digits (e.g., `cd001`, `cd999`, `cd1000`).
