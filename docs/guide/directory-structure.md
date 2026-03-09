# Directory Structure

Data repositories follow this structure:

```text
my-cryo-data/
├── components.yaml              # Component catalog
├── templates/
│   ├── control_module.yaml      # Control line module template
│   ├── readout_send_module.yaml # Readout send line module template
│   └── readout_return_module.yaml # Readout return line module template
├── <cryo-name>/
│   └── <YYYY>/                  # Year group
│       ├── cd001/               # Cooldown directory
│       │   ├── metadata.yaml
│       │   ├── chip.yaml
│       │   ├── components.yaml  # Per-cooldown (optional)
│       │   ├── control.yaml
│       │   ├── readout_send.yaml
│       │   ├── readout_return.yaml
│       │   └── cooldown.yaml    # Resolved bundle
│       └── cd002/
│           └── ...
```

## Key Concepts

- **`components.yaml`** **(required)** — Shared component catalog defining all RF/microwave parts used in wiring configurations. All components must be registered here and referenced by key name in wiring files
- **`templates/`** — Module templates that define default stage configurations per line type. Each template file uses the same format as the `modules` section in wiring files, so they can be imported and shared across cooldowns
- **`<YYYY>/`** — Year group directory (e.g., `2026`)
- **`cdNNN/`** — Cooldown directory with auto-incrementing ID (e.g., `cd001`, `cd002`)
- **`chip.yaml`** — Chip metadata (name, number of qubits)
- **`metadata.yaml`** — Cooldown metadata (ID, date, cryo, operator, purpose)
- **`cooldown.yaml`** — Resolved bundle with all modules expanded and components resolved
