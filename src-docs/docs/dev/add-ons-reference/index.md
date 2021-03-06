# Scripting API reference

[*Rainbox Laboratory*](https://rainboxlab.org) provides a reference implementation of the API in *Python* and *Adobe ExtendScript*.

Other APIs may be developped, in which case all these APIs on all programming/scripting language should implement this reference, with the same classes, attributes and methods.

[TOC]

As this document is referring to different languages, it uses general terms which may be different than what is usually used in specific languages.

## Classes

This is the comprehensive list of available classes.

| Class | Inheritance | Description |
| ---- | ---- | ---- |
| [Ramses](ramses.md) | | The main class. One (and only one) instance globally available, instantiated during init time. |
| [RamApplication](ram_application.md) | [RamObject](ram_object.md) | A class representing an application used in the pipeline (like *Blender*, *Nuke*, *Krita*, *Photoshop*...). |
| [RamAsset](ram_asset.md) | [RamItem](ram_item.md) | An asset. |
| [RamAssetStep](ram_assetstep.md) | [RamStep](ram_step.md) | A step in the production of the assets of the project. |
| [RamFileType](ram_filetype.md) | [RamObject](ram_object.md) | A class representing file types and their association with [RamApplications](ram_application.md). |
| [RamItem](ram_item.md) | [RamObject](ram_object.md) | Base class for [RamAsset](ram_asset.md) and [RamShot](ram_shot.md). An item of the project, either a general item, an asset or a shot. |
| [RamObject](ram_object.md) | | The base class for most of Ramses objects. |
| [RamProject](ram_project.md) | [RamObject](ram_object.md) | A project handled by Ramses. Projects contains general items, assets and shots. |
| [RamShot](ram_shot.md) | [RamItem](ram_item.md) | A shot. |
| [RamShotStep](ram_shotstep.md) | [RamStep](ram_step.md) | A step in the production of the shots of the project. |
| [RamState](ram_state.md) | [RamObject](ram_object.md) | The state of a step (like "Waiting for approval", "Approved", etc.). |
| [RamStatus](ram_status.md) | | A state associated to a comment, the user who changed the state, etc. |
| [RamStep](ram_step.md) | [RamObject](ram_object.md) | Base class for [RamAsset](ram_asset.md) and [RamShot](ram_shot.md). A step in the production of the shots or assets of the project. |
| [RamStepStatus](ram_stepstatus.md) | | A history of RamStatus for a given step. |
| [RamUser](ram_user.md) | [RamObject](ram_object.md) | The class representing users. |

## Implementation

Some of the elements described in this documentation have to be interpreted depending on the language used in the implementations of the Ramses API.

### Enumerated Values

#### Python and ExtendScript

Should be a string with the name of the value, enclosed in single quotes to differenciate them from other strings. Example: `'ADMIN'`, `'STANDARD'`.

