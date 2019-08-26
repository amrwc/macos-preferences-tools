# macOS Preferences Tools

Tools for determining macOS system preferences from the low, plist domains level. They help analysing what is being changed through the System Preferences.app GUI.

## Usage

_Please note: when the preferences in the user's home folder seem not to change when using System Preferences.app, try using the `--root` flag for backups._

```bash
# Save all the current preferences
./make_backup --before [--root]
```

Open System Preferences.app, do the changes you want to be able to perform in the script, and close the app.

```bash
# Save the new preferences
./make_backup --after [--root]
# Check for changes
./compare_full_backups [--root]
```

The above will tell which domains have changed. The next step is to decompile them to XML and compare them to see which key-value pairs have changed.

<!-- TODO: add optional --root flag when the support for it is added to the plist_compare script -->

```bash
./plist_compare <domain_name> code
```
