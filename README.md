# Crestron-Home-Extension-Driver-Template

These files make up a template for writing extension drivers for Crestron Home. Normally this project is shared as a full Visual Studio solution zip, but the complete solution is larger than GitHub's file-size limits.

## Converting this template into a production Crestron Home driver

This repository is the starting point. A functioning driver still requires device-specific transport logic, protocol parsing, command/feedback wiring, and metadata/UI completion.

## Canonical documentation context

Use [`docs/CODEX_CONTEXT.md`](docs/CODEX_CONTEXT.md) as the primary source of truth for SDK links, architecture notes, UI contract expectations, and implementation guidance.

Use [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) for a template-level breakdown of runtime layers, responsibilities, data flow, and packaging model.

When in doubt, update `docs/CODEX_CONTEXT.md` first and keep this README concise.

## Optional docs still helpful

Please share direct links to the exact pages for:

1. Optional: transport implementation examples for your specific target protocol/device class (helpful for production behavior, but not required for using this basic template).

Note: Packaging/Manifest Utility steps can be handled at the end and are not required to start core driver implementation.

## Implementation plan mapped to this template

1. Define v1 feature scope for a target device (power, inputs, volume, mute, feedback/events).
2. Build device transport/session handling in `Device_Name_Transport.cs`.
3. Implement command format + response parsing in `Device_Name_Protocol.cs`.
4. Connect lifecycle, actions, and feedback publication in `Device_Name.cs`.
5. Finalize runtime settings/metadata in `Settings_Data.cs` and `Device_Name.json`, and add UI translation strings in `en-US.json`.
6. Finalize UI metadata in `UiDefinition.xml`.
7. Validate on hardware (or an emulator) and iterate on timing/error-handling edge cases.
8. Perform end-of-cycle packaging/manifest steps after functional behavior is complete.

## Immediate next step from the docs provided

Using the "Create a Project," "Extension Drivers," "UI Files," and full SDK API reference, we can now begin implementation by replacing template placeholders with concrete driver identity values and scaffolding required driver classes/methods directly against the API docs before filling in transport/protocol specifics.

## Device details needed before coding

- Manufacturer + exact model number(s).
- Firmware version(s) to support.
- Official protocol/API reference for the device.
- Required commands/feedback for v1.
- Known quirks (rate limits, login/auth flow, warmup timing, unsolicited feedback behavior).
