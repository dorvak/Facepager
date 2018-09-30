# How to build Facepager
## Windows

Setup Facepager to run in your environment, see src/readme.txt

Install NSIS

Adjust paths and version numbers in
- src/setup_windows.py
- Facepager_Setupscript.nsi
- build.bat

Run build.bat

## OS X El Capitan

Setup Facepager to run in your environment, see src/readme.txt

Adjust paths and version numbers in
- src/setup_osx.py
- build.command

Grant execute permissions to build.command by typing in terminal:
  $chmod a+rwx build.command

To show hidden files execute in terminal, then Alt+RightClick Finder and choose "Relaunch"
    $defaults write com.apple.finder AppleShowAllFiles YES

To edit files install text editor, e.g. sublime text	
Run build.command by double clicking in Finder or in terminal

Hints for solving errors:
https://stackoverflow.com/questions/16131500/py2app-error-in-find-needed-modules-typeerror-nonetype-object-has-no-attribu

Hints for solving errors:
After running py2app run the built from command line:
~/Documents/GitHub/Facepager/dist/Facepager.app/Contents/MacOS/Facepager

# How to deploy builds

_Don't forget to adjust the tag name and message below_

- Create a git tag on the command line with `git tag -a v3.9.2 -m 'Version 3.9.2'`
- Upload the tag to GitHib with `git push origin v3.9.2`
- For major releases draft a new release on GitHub, for minor releases edit the last release.
- Enter the tag into the corresponding field, edit release notes, upload binary files.