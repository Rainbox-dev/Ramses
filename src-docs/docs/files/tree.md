# Folder Structure: the Ramses Tree

One of Ramses' goals is to manage all your files and folders; sometimes, you may still need to manually add, remove, or edit files and folders through your explorator, in which case you should always try to respect the *Ramses Tree* described here.

This document will also help you find your files should Ramses be unavailable for some reason.

[TOC]

## Introduction

All folders inside the *Ramses Tree* follow the Ramses [Naming Scheme](naming.md).

The folders used by Ramses can be located either locally or on remote computers and servers. The supported protocols (SMB, FTP...) may vary depending on the platform (read below for more information).

Ramses includes a system of *alternative trees*, which means you can use different paths to folders used by Ramses, and that it is compatible with virtually all syncing applications (Dropbox, Syncthing, Synology...), wether they are automatic or manual (like backup tools).

If a specific file or folder is not found in the *main tree*, Ramses will automatically look for it in the *alternative trees* and try to sync (i.e. copy in the *main tree*) them.

!!! tip
    For best performance, it is advised to work with local files, and use remote locations only as *alternative trees*; in conjunction with a syncing tool like [*Syncthing*](https://syncthing.net/) or the *Synology Drive* application for example, it is both easy, safe and powerful to keep a shared copy of the projects while working locally.

### Remote files on Windows

Ramses should be able to access files located on remote locations using the *Samba* (*SMB*) protocol, using standard URL starting with `\\server-name`.

Another way to access remote locations, which enables *FTP* and other protocols support, is to use *Windows Network Drives* to mount the remote locations. To make it easy to deploy Ramses on several devices, they should all use the same letter for the network drive.

### Remote files on Unix-like Systems (Linux, Mac OS)

The quickest and easiest way to use Ramses on remote folders on Unix-like systems is to automatically mount the remote locations in a specific folder. This can work for a lot of different protocols (*Samba*, *FTP(s)*, *SFTP*, *NFS*...)

## The Ramses Folder

The easiest way to use Ramses to manage all your projects is to define a root folder for all Ramses projects, where Ramses will create a subfolder for each project.

This Ramses folder is also used to store user specific files, some configuration files, etc.

Nevertheless, you can always choose another folder to store a specific project, outside of the Ramses Folder.

```sh
- Ramses Folder
    - Config # Configuration files
    - Projects # All projects
        - Project01 # First project
        - Project02 # Second project
        - ...
    - Users # User files
        - User01 # Files for a single user
        - User02
        - ...
```

## The Project Folder

These are the contents of the Project folder:

```sh
- PROJECTID # Root
    - 00-ADMIN # Project administration
    - 01-PRE-PROD # Pre-production steps
    - 02-PROD # Production steps
    - 03-POST-PROD # Post-production steps
    - 04-ASSETS # All the Assets
    - 05-SHOTS # All the Shots
    - 06-EXPORT # Media files
```

The root folder of a project only contains other folders and no files.

The subfolder in the root folder are numbered to help sorting them and quickly find them.

Here is an example of a typical project tree, without showing the details in the working directories nor any file.

```sh
- PROJECTID # Root
    - 00-ADMIN
    - 01-PRE-PROD
        - PROJECTID_SCRIPT # Pre production step
        - PROJECTID_STORYBOARD
    - 02-PROD
        - PROJECTID_MOD # Common files for the mod step
        - PROJECTID_RIG # Common files for the rig step
        - PROJECTID_TEX # Common files for the tex step
        - PROJECTID_ANIM # Common files for the anim step
        - PROJECTID_LIGHT # Common files for the light step
        - PROJECTID_COMP # Common files for the comp step
    - 03-POST-PROD
        - PROJECTID_EDIT # Post production step 
    - 04-ASSETS 
        - Characters # A Group of Assets
            - PROJECTID_A_TRISTAN # An Asset
                - PROJECTID_A_TRISTAN_DESIGN # An asset production step
                - PROJECTID_A_TRISTAN_MOD # An asset production step
                - PROJECTID_A_TRISTAN_RIG # An asset production step
                - PROJECTID_A_TRISTAN_TEX # An asset production step
            - PROJECTID_A_ISOLDE # An Asset
        - Props # A Group of Assets
        - Sets # A Group of Assets
    - 05-SHOTS
        - PROJECTID_S_01-001 # A Shot
            - PROJECTID_S_01-001_ANIM # A shot production step
            - PROJECTID_S_01-001_LIGHT # A shot production step
            - PROJECTID_S_01-001_COMP # A shot production step
        - PROJECTID_S_01-002 # A Shot
        - PROJECTID_S_01-003 # A Shot
        - PROJECTID_S_02-001 # A Shot
    - 06-EXPORT
```

## A working folder

A folder containing working files is always organised the same way.

Here is an example for the modelling step of the asset called *Tristan*.

```sh
- PROJECTID_A_TRISTAN_MOD # The working folder, subfolder of the asset folder.
    - PROJECTID_A_TRISTAN_MOD.blend # The main file for modelling Tristan (on Blender)
    - PROJECTID_A_TRISTAN_MOD_Sculpt.blend # Another resource
    - ramses_versions # The versionning folder, handled by Ramses.
        - PROJECTID_A_TRISTAN_MOD_wip001.blend # A WIP version
        - PROJECTID_A_TRISTAN_MOD_wip002.blend
        - PROJECTID_A_TRISTAN_MOD_chk003.blend # The version which has to be checked by the lead
        - PROJECTID_A_TRISTAN_MOD_ok004.blend # The validated version
        - PROJECTID_A_TRISTAN_MOD_pub005.blend # The version which has been published
        - PROJECTID_A_TRISTAN_MOD_Sculpt_v001.blend # The first version of a resource
        - PROJECTID_A_TRISTAN_MOD_Sculpt_v002.blend # The second version of a resource
    - published
        - PROJECTID_A_TRISTAN_MOD.blend # The working file as it was when publishing
        - PROJECTID_A_TRISTAN_MOD.abc # The published export (an *Alembic* file)
    - preview
        - PROJECTID_A_TRISTAN_MOD.jpg # A file for previewing the modelling
        - PROJECTID_A_TRISTAN_MOD.mp4 # A file for previewing the modelling
```

The *ramses_versions* subfolder contains the versionning and history of the work.

The *published* subfolder contains the published and exported files to be used by other steps.

The *preview* subfolder contains the files for previewing the current work, like videos or images. These files may be used by Ramses to generate thumbnails. Ramses is also able to list, preview, and play these files (if their format is standard and supported).

!!! important
    The working file and published files do not include the version in their names, and the versionning and history are hidden in a *ramses_versions* subfolder. This way, there can be no mistake about what file to open or import.

!!! note
    Only Ramses should access the *ramses_versions* subfolder and it should not be needed for the user to manipulate these files.

!!! tip
    When backuping a project, only the files in the *published* subfolder may be kept.