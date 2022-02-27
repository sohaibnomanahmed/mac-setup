# mac-setup
My personal Mac setup

## Install Homebrew
can be installed from: https://brew.sh
Then install wget as described at the website and maybe flutter via fvm docs: https://fvm.app. Flutter uses analytics, not sure how to remove them from fvm.

## Install required application
Install applications like XCode from Appstore and VSCode, Android Studio from the webiste

## Git setup
1. Get an access token from the github.com website for your account, Mac will for now auto remember the token so no need to keep a copy. This also will work for VSCode
2. To use github from VSCode, you need to setup username and email in config. Config log will show you how after you try to commit from VSCode. Config email will also connect to your github account, or else it is anonymous.

## VSCode
Install packages to make VSCode better, for icons improvement (Material Design Icons) is a choise. For color sheme (One Dark Pro) is a good choise. Install language spesific packages like Flutter whihc will also install Dart. Python and Jupyter Notebook, for some reason it recommend you to install python3 via brew, but macOS already ships with python3? Not sure whats happening here.

## FVM
Install a the stable release using
```
fvm install stable
```
If you have a repo created without fvm, go to that directory and use the command below or another version there, this will create a .fvm in the directory
```
fvm use stable
```
Setup fvm for VSCode with chnaging the settings file via CMD+SHIFT+P and choose "Open Settings (JSON)". Then copy paste this code, always chakc with the documentation to use the latest versions.
```
{
  "dart.flutterSdkPath": ".fvm/flutter_sdk",
  // Remove .fvm files from search
  "search.exclude": {
    "**/.fvm": true
  },
  // Remove from file watching
  "files.watcherExclude": {
    "**/.fvm": true
  }
}
```
