# mac-setup
My personal Mac setup

## Install Homebrew
can be installed from: https://brew.sh
Then install wget as described at the website, Activity Monitor can be used to monitor the system htop is not needed.

To update packages use
```
brew update
brew upgrade
```

## Oh-My-Zsh
First install Oh-My-Zsh as described on their website: https://ohmyz.sh
Then add the the autosuggestions plugin by following the steps on their github: https://github.com/zsh-users/zsh-autosuggestions in the INSTALL.md file, you could install it from homebrew as well (https://formulae.brew.sh/formula/zsh-autosuggestions), but the github version seems cleaner as it adds it to the plugins.

Find a suitable theme here https://travis.media/top-12-oh-my-zsh-themes-for-productive-developers/ previously have I choosen "simple"

lastly remove the ls colors if wanted, this can be done in the .zshrc file by removing the comment for LSCOLORS lik this
```
# Uncomment the following line to disable colors in ls.
DISABLE_LS_COLORS="true"
```

## Python
Also to not mess up the python2 and python3 versions on the mac, we can install python3 throgh pyenv. The reason on why and how to use pyenv instead of homebrew is stated in a later answer here: https://stackoverflow.com/questions/60298514/how-to-reinstall-python2-from-homebrew. Install the latest version listed here https://www.python.org/downloads/. I still dont really get the reason for this and therefore use brew instead.

```
brew install python3
```

## Install required application and frameworks
Install applications like XCode from Appstore and VSCode, Android Studio from the webiste. To keep Android Studio and VSCode upto date install it through homebrew
```
brew install --cask flutter
brew install --cask android-studio
brew install --cask visual-studio-code
```
If issues updating cask occurs read the following: https://stackoverflow.com/questions/31968664/upgrade-all-the-casks-installed-via-homebrew-cask. Also if need for package managers you have for flutter fvm docs: https://fvm.app.

## Git setup
1. Get an access token from the github.com website for your account, Mac will for now auto remember the token so no need to keep a copy. This also will work for VSCode
2. To use github from VSCode, you need to setup username and email in config. Config log will show you how after you try to commit from VSCode. Config email will also connect to your github account, or else it is anonymous.

## VSCode
Install packages to make VSCode better, for icons improvement (Material Design Icons) is a choise. For color sheme (One Dark Pro) is a good choise. Install language spesific packages like Flutter whihc will also install Dart. Python and Jupyter Notebook.

Also change the settings, to get there use [CMD+,] or press the wheel in the bottom left. Change the auto save to "After Delay", this should save the file after 1000ms, turn on word wrap and remove the check mark for Flutter Hot Restart On Save. Since you have auto save on this will trigger hot restart when ever you make a change, which is not wanted and by turning it off, you decide when you want to hot restart. 

## Development Folder
Before creating projects its nice, to set up a Developer folder where you can structure your project. One idea could be two subfolders for work and personal projects. Make the developer folder in the home directory by
```
mkdir Developer
```

## Flutter
To run your flutter project please read the documentation at: https://docs.flutter.dev/
But generally after installing fvm and Xcode and Android Studio, run this command from your repo
```
fvm flutter doctor 
```
You probably need to complete the Xcode installation these 3 commands, also sccording to this answer you should install cocoa pods using brew instead of gem: https://stackoverflow.com/questions/65570441/react-native-should-i-install-cocoapods-with-gem-or-homebrew
```
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -runFirstLaunch
#sudo gem install cocoapods

brew install cocoapods
```
And to complete the Android Studio installment use these commands after fixing missing command-line tools, the solution is here: https://stackoverflow.com/questions/68236007/i-am-getting-error-cmdline-tools-component-is-missing-after-installing-flutter
```
fvm flutter doctor --android-licenses
```
To connect to an android device open Andorid Studio and create a Virtual emulator, for iOS run the command
```
open -a Simulator
```
To create a new project remember to add the desired package name, so you dont need to change it later s example.com is not useable. Also to create a project using fvm a version needs to be used. Since the versions are only in the project a work around is to use a version in the current folder with --force
```
fvm use <VERSION> --force
```
Then create the project and later remove the .fvm folder from the folder above the project. Rember to call the fvm use [VERSION] inside the project folder.
```
fvm flutter create --org com.yourdomain appname
```
Another option is to choose a global version, add that to the PATH, then create the project from the global version. The PATH should be added to your .zshrc file.
```
fvm global <VERSION>
export PATH="$PATH:/Users/sohaibahmed/fvm/default/bin"
flutter create appname
```
Lastly add the cached flutter version created by fvm use to the .gitignore file. Since this is not auto done rn
```
.fvm/flutter_sdk
```
## Java
To make publishing keys for android, when you want to publish your app to app stores. Java is needed, to get java install it through brew steps are from this stie: https://mkyong.com/java/how-to-install-java-on-mac-osx/
```
brew install java
sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
```
