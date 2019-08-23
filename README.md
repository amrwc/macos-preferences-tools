# macOS Preferences Tools

## Set preferences through command line

```bash
# Get a domain's current value
defaults read <domain>
# Get a domain's value type
defaults read-type <domain>
# Set a domain's value
defaults write <domain> <value>
# More details
man defaults
```

## Find out what is being changed by the System Preferences.app

Source: https://apple.stackexchange.com/a/79765

Remember to quit System Preferences.app before applying the change using `defaults`.

```bash
osascript -e 'tell application "System Preferences" to quit'
```

```bash
# Save all the current preferences
./make_backup before
```

Open System Preferences.app and do the changes you want to be able to perform in the script.

```bash
# Save the new preferences
./make_backup after
# Find out which files have changed
./compare_full_backups
```

The above will tell which files have changed. The next step is to decompile them to XML and compare them to see which key-value pair has changed.

```bash
./plist_compare <domain_name> code
```

You can also save and compare the domain's before and after states directly from source.

```bash
plutil -convert xml1 -o /dev/stdout ~/Library/Preferences/<domain_name> > before
plutil -convert xml1 -o /dev/stdout ~/Library/Preferences/<domain_name> > after
code --diff before after
```

## Idioms for NSGlobalDomain

- kCFPreferencesAnyApplication,
- .GlobalPreferences – it's a file name, therefore if it doesn't exist, `defaults` will fail.
