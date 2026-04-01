# CODEX_CONTEXT.md

## Purpose

Primary Codex reference for Crestron Home Extension Driver development using the Crestron Certified Driver SDK v1.

Use this file first when generating or modifying driver code.

It links the most relevant official docs for:

* Driver architecture and lifecycle
* Required Simpl# classes and interfaces
* UI contract (`UiDefinition.xml` + `en-US.json`)
* Driver JSON schema and metadata
* API reference and best practices

---

## Start Here

* [Driver SDK v1 Landing Page][sdk-root] - Entry point for all SDK documentation
* [Create a Project][create-project] - Required Simpl# classes, interfaces, and project structure

---

## Driver Architecture

* [Extension Drivers Overview][extension-drivers] - How Crestron Home extension drivers work
* [SDK Architecture][sdk-architecture] - Framework design, communication model, and implementation guidance

---

## UI Contract (Critical)

* [UI Files Reference (`UiDefinition.xml`)][ui-files] - Layouts, controls, bindings, navigation
* [UI Translations (`en-US.json`)][ui-translations] - Translation keys and formatting rules

`UiDefinition.xml` is the contract between driver code and UI.

* Property names must match exactly
* Bindings like `{PropertyName}` must exist in code
* Translation keys (`^`) must exist in `en-US.json`

---

## Driver JSON (Packaging and Metadata)

* [Driver JSON Schema][driver-json-schema] - Required structure for driver metadata
* [Driver JSON API Details][driver-json-api] - Property-level definitions and behavior

Use this when:

* Defining device metadata
* Configuring communication settings
* Debugging packaging issues (`.pkg`)

---

## API Reference (Simpl#)

* [Crestron Device Driver SDK API][sdk-api] - Full class and member reference

Use this for:

* `AExtensionDevice`
* `ATransportDriver`
* `ABaseDriverProtocol`
* Extension UI properties
* Communication handling

---

## Repo File Map (This Template)

* `Device_Name.cs` - Driver lifecycle, actions, and feedback wiring
* `Device_Name_Transport.cs` - Transport/session and connection behavior
* `Device_Name_Protocol.cs` - Command formatting and response parsing
* `Settings_Data.cs` - Runtime settings model
* `Device_Name.json` - Driver metadata and communication schema
* `UiDefinition.xml` - UI structure and bindings
* `en-US.json` - UI translation strings

---

## Quick Usage Guide

When working with Codex:

* Creating a new driver -> Start with **Create a Project**
* Building transport/protocol -> Use **API Reference + SDK Architecture**
* Fixing UI issues -> Use **UI Files Reference**
* Fixing bindings -> Compare **UiDefinition.xml** with C# property names
* Packaging/debugging -> Use **Driver JSON Schema**
* General improvements -> Review **Best Practices**

---

## Best Practices

* [Crestron Driver SDK Best Practices][best-practices] - Official guidance for structure, performance, and reliability

---

## References

[sdk-root]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/Driver-SDK-V1.htm
[create-project]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/Create-a-Driver/Create-a-Project.htm
[extension-drivers]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/Create-a-Driver/Device-Types/Extensions/Extension-Drivers.htm
[ui-files]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/Create-a-Driver/Device-Types/Extensions/UI-Files.htm
[ui-translations]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/Create-a-Driver/Device-Types/Extensions/UI-Files.htm#Translations
[sdk-api]: https://sdkcon78221.crestron.com/downloads/CrestronCertifiedDriversAPI/html/R_Project_Crestron_Certified_Drivers_SDK_Documentation.htm
[driver-json-schema]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/API-Reference/Driver-JSON-Schema/Driver-JSON-Schema.htm
[driver-json-api]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/API-Reference/Driver-JSON-Schema/API/API.htm
[sdk-architecture]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Driver-SDK-V1/SDK-Framework/SDK-Architecture.htm
[best-practices]: https://sdkcon78221.crestron.com/sdk/Crestron_Certified_Drivers_SDK/Content/Topics/Best-Practices/Best-Practices.htm

---
