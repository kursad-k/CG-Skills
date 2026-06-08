# Blender - Addons

**Pages:** 2

---

## Add-ons¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/addons.html

**Contents:**
- Add-ons¶
- Filtering Add-ons¶
- Add-on Settings¶
- Enabling & Disabling Add-ons¶
- Add-on Information¶
  - Add-on Preferences¶
- Installing Legacy Add-ons¶

The Add-ons section lets you manage secondary scripts, called “Add-ons” that extends Blender’s functionality. Most of the time you can get add-ons as part of the Extensions system.

In this section you can search, install, enable and disable Add-ons.

Blender Preferences Add-ons section.¶

If the Add-on does not activate when enabled, check the Console window for any errors that may have occurred.

Blender comes with some preinstalled Add-ons already, ready to be enabled. But you can also add your own, or any interesting ones you find on the web.

Shows only enabled add-ons for the current Category.

Add-ons are assigned categories by what areas of Blender they affect.

Scan extension & legacy add-ons for changes to modules & meta-data (similar to restarting). Any issues are reported as warnings.

Install an extension from a .zip package. This is installed to a Local Repository and no updates will be available.

This can also be used to install legacy Add-ons, for more information see: Installing Legacy Add-ons.

To enable or disable an add-on check or uncheck the box to the right of the add-ons.

The add-on functionality should be immediately available.

You can click the arrow at the left of the add-on box to see more information, such as its location, a description and a link to the documentation. Here you can also find a button to report a bug specific of this add-on.

Some add-ons may have their own preferences which can be found in the Preferences section of the add-on information box.

Some add-ons use this section for example to enable/disable certain functions of the add-on. Sometimes these might even all default to off. So it is important to check if the enabled add-on has any particular preferences.

To install legacy add-ons, click the Install from Disk menu item and select the add-on’s .py file (if it has only one such file) or its .zip file.

The add-on will not be automatically enabled after installation; click the checkbox to do that.

Scans the Add-on Directory for new add-ons.

While this screen doesn’t allow installing a folder-based addon with loose .py files, you can still do so by adding it as a Script Directory:

Create an empty directory in a location of your choice (e.g. my_scripts).

Add a subdirectory under my_scripts called addons (it must have this name for Blender to recognize it).

Place your addon folder inside this addons folder.

Open the File Paths section of the Preferences.

Add a Script Directories entry pointing to your script folder (e.g. my_scripts).

Save the preferences and restart Blender for it to recognize the new add-on location.

The add-ons in this folder will automatically become available; all you need to do is enable them.

---

## Get Extensions¶

**URL:** https://docs.blender.org/manual/en/latest/editors/preferences/extensions.html

**Contents:**
- Get Extensions¶
- Installing Extensions¶
- Updating Extensions¶
- Enable/Disable¶
- Extension Settings¶
- Filter by Type¶
- Repositories¶
  - Remote Repository¶
  - Local Repository¶

The Get Extensions section lets you install and manage extensions preferences.

Blender Preferences Extensions section.¶

To learn about extensions and how to create them, refer to the Extensions page.

There are different ways to install an extension:

Drag the installation URL into Blender.

Search for the extension name and click on Install.

Use the drop-down menu in the top right, or drag-and-drop an extension .zip package into Blender.

Any installed extension can be removed. This is a permanent change, though. To stop an extension temporarily, it is better to Disable it instead.

See network troubleshooting for issues connecting to remote repositories.

You need to manually check for available updates. Once an update is found, Blender will let you update any of the available extensions.

The current available version of an extension on the repository will always be considered the latest version.

Once an extension is installed it can be disabled (or re-enabled) as part of the user preferences. Some extension types do not support this, and will always be shown as enabled.

If the Add-on does not activate when enabled, check the Console window for any errors that may have occurred.

Opens extensions.blender.org in a web browser.

Manually check the online repositories for available updates.

Scan extension & legacy add-ons for changes to modules & meta-data (similar to restarting). Any issues are reported as warnings.

Update all the extensions that have an update available.

Install an extension from a .zip package. This is installed to a Local Repository and no updates will be available.

This can also be used to install legacy Add-ons, for more information see: Installing Legacy Add-ons.

Or show only extensions of a single type:

By default Blender has a Remote Repository pointing towards the Official Blender Extensions Platform and two Local Repositories.

In the cases where more repositories are needed (e.g., to access third party extension platforms), new repositories can be added.

To add new repositories click on the + icon:

Add a repository from a URL.

Add a repository which will be managed by the user (to be used with Install from Disk).

To remove repositories click on the - icon:

Remove an extension repository.

Remove a repository and delete all associated files when removing.

These changes are permanent and cannot be reversed.

Remote repository with support for listing and updating extensions.

Allows Blender to check for updates upon launch. When updates are available a notification will be visible on the status bar.

Personal access token, may be required by some repositories.

A repository managed manually by the users.

There are two types of local repositories. By default new local repositories are added as User repositories. This is what you want most of the time.

After creating a repository they can be changed in the Advanced options to have a source System. These repositories are intended to bundle extensions with Blender, to make it portable.

---
