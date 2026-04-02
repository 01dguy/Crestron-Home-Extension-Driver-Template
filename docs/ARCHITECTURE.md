# Architecture

## Scope
This document describes the architecture of this repository as a reusable Crestron Home Extension Driver template. It is intentionally generic so it can support many device categories (AV, lighting, HVAC, sensors, and other extension-capable integrations).

All statements below are based on files currently present in this repo.

## Main Project Structure
- `Device_Name.cs`: top-level extension device class (`AExtensionDevice`) and orchestration layer.
- `Device_Name_Protocol.cs`: protocol/state layer (`ABaseDriverProtocol`) where polling, parsing, and device-specific command logic belong.
- `Device_Name_Transport.cs`: transport layer (`ATransportDriver`) for network/serial communication implementation.
- `Settings_Data.cs`: persisted settings model used to save and restore user/runtime configuration.
- `Device_Name.json`: driver metadata and communication schema used by the Crestron platform.
- `IncludeInPkg/UiDefinitions/UiDefinition.xml`: extension UI contract (layouts, controls, bindings, actions).
- `IncludeInPkg/Translations/en-US.json`: localization strings referenced by `UiDefinition.xml`.
- `docs/CODEX_CONTEXT.md`: curated SDK/documentation reference for implementation guidance.

## Architectural Layers
The template is organized into three core runtime layers plus configuration artifacts.

1. Device orchestration layer (`Device_Name`)
- Owns Crestron lifecycle (`Initialize`, `Connect`, `Disconnect`, `Dispose`).
- Defines UI-exposed properties and handles UI actions/commands.
- Instantiates and wires transport and protocol.
- Coordinates persisted settings load/save.

2. Protocol/state layer (`Device_Name_Protocol`)
- Encapsulates device protocol behavior independent of UI layout.
- Owns polling cadence and reaction to inbound data.
- Translates raw transport traffic into normalized driver state.
- Calls back into device layer for UI refresh/event signaling.

3. Transport layer (`Device_Name_Transport`)
- Encapsulates connection mechanics and send/receive mechanics.
- Hides communication medium details from protocol and device layers.
- Maintains connection state used by upper layers.

4. Configuration and package artifacts
- `Device_Name.json` describes capabilities and communication defaults.
- UI XML + translation JSON define UX and labels.
- `Settings_Data` provides persisted runtime preferences/state.

## Key Classes And Responsibilities

### `Device_Name` (orchestration and UI bridge)
- Creates driver property definitions that back UI bindings.
- Handles command dispatch from UI actions.
- Loads persisted settings before use and saves updates on command.
- Starts/stops protocol behavior in connect/disconnect lifecycle.
- Maintains high-level driver status/events for Crestron Home integration.

### `Device_Name_Protocol` (protocol engine)
- Manages auto-polling and protocol lifecycle.
- Processes responses/notifications from transport.
- Updates device-facing state and triggers UI refresh callbacks.
- Accepts user attributes (e.g., IDs/endpoints) and maps them to runtime state.

### `Device_Name_Transport` (I/O boundary)
- Implements `Start`, `Stop`, and `SendMethod` contract.
- Tracks and reports connection state.
- Serves as the abstraction boundary for Ethernet/serial/cloud transport details.

### `Settings_Data` (persisted settings contract)
- Defines values that should survive restarts/reconnects.
- Provides default initialization and update/save model.
- Keeps persistence concerns out of protocol and transport code.

## Runtime Flow (Template-Level)
1. Platform initializes driver instance.
2. `Device_Name.Initialize()` configures logging, properties, transport, and protocol.
3. `Connect()` loads persisted settings and starts protocol.
4. Protocol starts polling and/or message handling.
5. Protocol updates runtime state and invokes UI update callback.
6. UI actions map to `DoCommand(...)`, which updates settings/state and persists when needed.
7. `Disconnect()` stops protocol and transport-related activity.

## UI Contract Model
`UiDefinition.xml` is a strict contract with code.

- Property bindings like `{SomeProperty}` must map to created driver properties.
- Command actions like `command:SomeCommand` must be handled in `DoCommand`.
- Translation keys prefixed with `^` must exist in `en-US.json`.

This separation allows UI iteration without changing transport/protocol internals, as long as binding/command contracts remain valid.

## Packaging Model
The template keeps package-bound UI assets under `IncludeInPkg/`:
- `IncludeInPkg/UiDefinitions/UiDefinition.xml`
- `IncludeInPkg/Translations/en-US.json`

This layout supports driver packaging workflows where non-code assets are included explicitly.

## Extension And Reuse Strategy
To build a concrete driver from this template:
1. Replace placeholder identity/metadata in `Device_Name.json`.
2. Implement real transport logic in `Device_Name_Transport.cs`.
3. Implement protocol command formatting/parsing in `Device_Name_Protocol.cs`.
4. Replace sample UI fields/commands with target-device controls.
5. Expand `Settings_Data` to include real persisted configuration.

## Conventions Observed In Template
- Separation of concerns is explicit between orchestration, protocol, and transport.
- UI updates are mediated through property updates and `Commit()`.
- Persistent settings are loaded/saved from device layer, not protocol layer.
- Template uses verbose logging hooks intended for early bring-up/debugging.

## Explicitly Unverified / Environment-Dependent Items
- Build execution is not validated in this repo snapshot (no `.sln`/`.csproj` included here).
- Actual SDK assembly resolution and packaging toolchain behavior depend on local Crestron SDK environment.
- Transport behavior is template-level and requires concrete implementation for production use.
