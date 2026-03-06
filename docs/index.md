# cryo-wiring-spec

Specification for dilution refrigerator wiring configuration data.

## Overview

This repository defines the YAML data format specification used across the cryo-wiring ecosystem.

- [cryo-wiring-cli](https://github.com/cryo-wiring/cli) — Core library + CLI (reference implementation of this spec)
- [cryo-wiring-app](https://github.com/cryo-wiring/app) — Web UI
- [cryo-wiring-template](https://github.com/cryo-wiring/template) — Data repository template

## Quick Links

- [Directory Structure](guide/directory-structure.md) — How data repositories are organized
- [Temperature Stages](guide/temperature-stages.md) — The 6 temperature stages
- [Component Types](guide/component-types.md) — Attenuators, filters, isolators, amplifiers
- [Line Configuration](guide/line-configuration.md) — Control, readout send, readout return lines
- [Examples](guide/examples.md) — Complete sample files
- [Schema Reference](reference/wiring-schema.md) — Auto-generated from JSON Schema
