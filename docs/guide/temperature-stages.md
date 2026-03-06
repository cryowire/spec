# Temperature Stages

Wiring is organized across 6 temperature stages of a dilution refrigerator, from room temperature down to the mixing chamber:

| Stage | Temperature | Description |
|-------|-------------|-------------|
| `RT` | ~300 K | Room temperature |
| `50K` | ~50 K | First cooling stage |
| `4K` | ~4 K | Pulse tube cooler stage |
| `Still` | ~0.8 K | Still plate |
| `CP` | ~0.1 K | Cold plate |
| `MXC` | ~10 mK | Mixing chamber |

## Signal Direction

- **Control / Readout Send lines** carry signals from `RT` down to `MXC` (input path)
- **Readout Return lines** carry signals from `MXC` back up to `RT` (output path)

Components are placed at specific stages to manage signal attenuation, filtering, isolation, and amplification along the wiring path.
