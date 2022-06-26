# mac-setup
My personal Mac setup

## Install Homebrew
can be installed from: https://brew.sh
Then install wget as described at the website and maybe flutter via fvm docs: https://fvm.app. Activity Monitor can be used to monitor the system htop is not needed.

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
Also to not mess up the python2 and python3 versions on the mac, we can install python3 throgh pyenv. The reason on why and how to use pyenv instead of homebrew is stated in a later answer here: https://stackoverflow.com/questions/60298514/how-to-reinstall-python2-from-homebrew. Install the latest version listed here https://www.python.org/downloads/.

```
brew install pyenv
pyenv install --list
pyenv install <latest-version>

pyenv global <latest-version>

PATH=$(pyenv root)/shims:$PATH
```


## Install required application
Install applications like XCode from Appstore and VSCode, Android Studio from the webiste. To keep Android Studio and VSCode upto date install it through homebrew
```
brew install --cask android-studio
brew install --cask visual-studio-code
```
If issues updating cask occurs red the following: https://stackoverflow.com/questions/31968664/upgrade-all-the-casks-installed-via-homebrew-cask

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

## FVM
Install a the stable release using
```
fvm install stable
```
To remove analytics from a spesific version installed run the following command
```
/Users/sohaibahmed/fvm/versions/<VERSION>/bin/flutter config --no-analytics
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

# Multiple Environments
Sometimes you need multiple environments, like working for a consultant company. Brew can be bloated and too much software can be downloaded. Currently I hvae two solutions for this, the first is to create a new user and install brew om the home directory for this user and use and add it to his PATH variables, then everything he installs is in hes own environment and the user can later be deleted. He will have his "own" mac in this regard more instructions for this approach can be found here: https://stackoverflow.com/questions/41840479/how-to-use-homebrew-on-a-multi-user-macos-sierra-setup

The second solution is to create somekind of environment system for brew, the idea for this came from this reddit post: https://www.reddit.com/r/osx/comments/70pa7u/separate_homebrew_environments/. I then created script in the .zshrc file for for creating and activating environments for my work projects the code is beneath. The current solution for deactivating is closing and starting a new terminal, but for reverting the path maybe this article can help: https://stackoverflow.com/questions/370047/what-is-the-most-elegant-way-to-remove-a-path-from-the-path-variable-in-bash

```
brew-create-env() {
	if [ -z $1 ]; then 
		echo "Usage: brew-create-env [NAME]"
		return 
	fi
	CACHE_DIR=$1
	test -d ~/Developer/Netcompany/env/$CACHE_DIR/Homebrew || git clone https://github.com/Homebrew/brew.git ~/Developer/Netcompany/env/$CACHE_DIR/Homebrew
}

brew-activate() {
	if [ -z $1 ]; then 
		echo "Usage: brew-activate [NAME]"
		return 
	fi
	CACHE_DIR=$1
	PATH=~/Developer/Netcompany/env/$CACHE_DIR/Homebrew/bin:$PATH

	export HOMEBREW_INSTALL_BADGE="🦍"
	export HOMEBREW_PREFIX="$HOME"
	export HOMEBREW_REPOSITORY="~/Developer/Netcompany/env/$CACHE_DIR/Homebrew"
	# Cask
	export HOMEBREW_CASK_OPTS="--appdir=${HOME}/Applications"
	# Completions
	fpath=($HOMEBREW_REPOSITORY/share/zsh/site-functions $fpath)

	PATH=$ZSH_CACHE_DIR/Homebrew/opt/openssl@1.1/bin:$PATH
	export PS1="($CACHE_DIR) "
}

brew-delete-env() {
	if [ -z $1 ]; then 
		echo "Usage: brew-delete-env [NAME]"
		return 
	fi
	CACHE_DIR=$1
	rm -rf ~/Developer/Netcompany/env/$CACHE_DIR
}

if [ -z $CACHE_DIR ]; then
	else PS1="($CACHE_DIR) %(!.%{$fg[red]%}.%{$fg[green]%})%~$(git_prompt_info)%{$reset_color%} "
fi
```
