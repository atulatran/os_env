# Mac OS Env

============

## Browsers

- Home page: [Google](https://www.google.com/)
- Extensions:
  - Google Translate
  - Grammarly
- Chrome
- Firefox
- Brave
- Tor

## Manage Files

- [OmniDiskSweeper](https://www.omnigroup.com/more)
- [Beyond Compare](https://www.scootersoftware.com/)
  - [Crack Beyond Compare](https://www.jianshu.com/p/93303b9fb21a)

## Offices

- Microsoft Offices (Word, Excel, ...)
- Libre Offices
- Unikey for Mac

## Manage Windows

- [Spectacle](https://www.spectacleapp.com/)

## Screenshot

- [LightShot](https://app.prntscr.com/en/index.html)
- [Flameshot](https://flameshot.org/)

## Package manager

- [Homebrew](https://docs.brew.sh/)
- Common Packages
  - [curl](https://formulae.brew.sh/formula/curl)
  - [wget](https://formulae.brew.sh/formula/wget)

## Terminals

- [iTerm2](https://iterm2.com/)
- [tmux](https://github.com/tmux/tmux/wiki)
  - Install

    ```bash
    brew install tmux
    ```

- [Vim](https://sourabhbajaj.com/mac-setup/Vim/README.html)
  - Install

    ```bash
    brew install vim
    ```

- [Zsh](https://www.zsh.org/)
  - [Installing ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

    ```bash
    brew install zsh
    ```

- [Oh My ZSH](https://ohmyz.sh/)
  - Install

    ```bash
    brew install zsh
    ```

## Teamworks

- [Slack](https://slack.com/)
- [Microsoft Teams](https://www.microsoft.com/en/microsoft-teams/group-chat-software)

## Video Meetings

- [Zoom](https://zoom.us/)
- [Meet](https://meet.google.com/)

## Version Control System

- [Git](https://git-scm.com/)
  - SSH
  - Host
  - [git-flow](https://danielkummer.github.io/git-flow-cheatsheet/)
- [Sourcetree](https://www.sourcetreeapp.com/)
- [GitKraken](https://www.gitkraken.com/)
- [SmartGit](https://www.syntevo.com/smartgit/)

## SDKs

### [Software Development Kit](https://sdkman.io/)

- [Installation SDKMAN](https://sdkman.io/install)

### [JDK](https://sdkman.io/jdks)

- Get a listing of Candidate Versions

    ```bash
    sdk list java
    ```

- [Azul Zulu](https://www.azul.com/downloads/?package=jdk)

    ```bash
    sdk install java 8.0.345-zulu
    sdk install java 11.0.16-zulu
    sdk install java 18.0.2-zulu
    ```

### [SDK Installation Candidates](https://sdkman.io/sdks)

- [Kotlin](https://kotlinlang.org/)

    ```bash
    sdk install kotlin
    ```

- [Groovy](http://www.groovy-lang.org/)

    ```bash
    sdk install groovy
    ```

- [Gradle](http://gradle.org/)

    ```bash
    sdk install gradle
    ```

- [Maven](https://maven.apache.org/)

    ```bash
    sdk install maven
    ```

- [Spring Boot](http://projects.spring.io/spring-boot/)

    ```bash
    sdk install springboot
    ```

- [Micronaut](http://micronaut.io/)

    ```bash
    sdk install micronaut
    ```

- [Apache JMeter](https://jmeter.apache.org/)

    ```bash
    sdk install jmeter
    ```

### [Flutter SDK](https://docs.flutter.dev/get-started/install/macos)

- Download the latest stable release of the Flutter SDK.
- Extract the file in the desired location.

    ```bash
    mkdir ~/development
    cd ~/development
    unzip ~/Downloads/flutter_macos_<flutter_sdk_latest_version>-stable.zip
    ```

- Path Environment
  - Determine the path of clone of the Flutter SDK.
  - Open (or create) the `rc file` for shell
    - `.bash_profile`
    - `.zshrc`
  - Add Dart - Flutter Path variables

    ```rc
    export PATH="$PATH:$HOME/development/flutter/common/flutter/bin/cache/dart-sdk/bin"
    export PATH="$PATH:$HOME/development/flutter/common/flutter/bin"
    ```

  - Refresh refresh the current window

    ```bash
    source $HOME/.<rc file>
    ```

### [Flutter Version Management](https://fvm.app/)

- Install use the Homebrew package manager for Mac OS.

    ```bash
    brew tap leoafarias/fvm
    brew install fvm
    ```

- Install as a pub package.

    ```bash
    dart pub global activate fvm
    ```

- List config

    ```bash
    fvm config
    ```

- Set cache path

    ```bash
    fvm config --cache-path <CACHE_PATH>
    ```

- View all SDKs

    ```bash
    fvm list
    ```

### [iOS Setup](https://docs.flutter.dev/get-started/install/macos#ios-setup)

- Install the latest stable version of Xcode.
- Configure the Xcode command-line tools to use the newly-installed version of Xcode.

    ```bash
    sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
    sudo xcodebuild -runFirstLaunch
    ```

- Make sure the Xcode license agreement is signed by either opening Xcode.

    ```bash
    sudo xcodebuild -license
    ```

- Set up the iOS simulator.
  - Find the Simulator

    ```bash
    open -a Simulator
    ```

- Install CocoaPods

    ```bash
    sudo gem install cocoapods
    ```

### [Android Setup](https://docs.flutter.dev/get-started/install/macos#android-setup)

- Download and install Android Studio.
- Installs the latest Android SDK, Android SDK Command-line Tools, and Android SDK Build-Tools.
- Set the directory that Android Studio is installed.

    ```bash
    flutter config --android-studio-dir <directory>
    flutter config --android-sdk <directory>
    ```

    ```bash
    flutter config --android-studio-dir "/Applications/Android Studio.app/Contents"
    ```

- Set up the Android emulator.
  - Enable VM acceleration on your machine.
    - [Configure VM acceleration on macOS](https://developer.android.com/studio/run/emulator-acceleration#vm-mac)
  - Launch `Android Studio`, click the `AVD Manager` icon, and select `Create Virtual Device` …
    - If do not have a project open, you can choose `Configure` > `AVD Manager` and select `Create Virtual Device`…
  - Choose a device definition and select `Next`.
  - Select one or more system images for the Android versions want to emulate, and select `Next`. An `x86` or `x86_64` image is recommended.
  - Under Emulated Performance, select `Hardware - GLES 2.0` to enable hardware acceleration.
  - Verify the AVD configuration is correct, and select `Finish`.
  - In Android Virtual Device Manager, click `Run` in the toolbar.
    - The emulator starts up and displays the default canvas for selected OS version and device.
- Agree to Android Licenses
  - Before can use Flutter, must agree to the licenses of the Android SDK platform.
  - This step should be done after you have installed the tools listed above.
  - Signing licenses

    ```bash
    flutter doctor --android-licenses
    ```

  - Review the terms of each license carefully before agreeing to them.

### [Node Version Manager](https://github.com/nvm-sh/nvm)

- Install

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    ```

- Path Environment
  - Open (or create) the `rc file` for shell.
    - `.bash_profile`
    - `.zshrc`
  - Add NVM Path variables.

    ```rc
    export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
    ```

  - Refresh refresh the current window.

    ```bash
    source $HOME/.<rc file>
    ```

- Verify that nvm has been installed.

    ```bash
    nvm -v
    ```

### [Node.js](https://nodejs.org/en/)

- List available versions.

    ```bash
    nvm ls-remote
    ```

- Install a specific version of node

    ```bash
    nvm install <node_version>
    ```

- Install the latest release of node

    ```bash
    nvm install node
    ```

- Use the installed version

    ```bash
    nvm use <node_version>
    ```

- Get the version of node

    ```bash
    node -v
    ```

### [Yarn Version Manager](https://yvm.js.org/docs/overview)

- Install

    ```bash
    brew install tophat/bar/yvm
    curl -s https://raw.githubusercontent.com/tophat/yvm/v2.4.3/scripts/install.sh | bash
    ```

### [Yarn](https://yarnpkg.com/)

- List installed yarn versions

    ```bash
    yvm list
    ```

- Install a specific version of Yarn

    ```bash
    yvm install <yarn_version>
    ```

- Install the latest version of Yarn

    ```bash
    yvm install latest
    ```

- Switch the current Yarn versions

    ```bash
    yvm use <yarn_version>
    yarn --version
    ```

- Show path to version used

    ```bash
    yvm which
    ```

### [TypeScript](https://www.typescriptlang.org/)

- Install

    ```bash
    npm install typescript --save-dev
    ```

### [Python Version Management - pyenv](https://github.com/pyenv/pyenv)

- References
  - [Managing Multiple Python Versions With pyenv](https://realpython.com/intro-to-pyenv/)
  - [Installing pyenv on macOS](https://binx.io/2019/04/12/installing-pyenv-on-macos/)
  -
- [Install the build dependencies](https://github.com/pyenv/pyenv/wiki)

    ```bash
    brew install openssl readline sqlite3 xz zlib tcl-tk
    ```

- Install pyenv

    ```bash
    brew install pyenv
    ```

- Install [pyenv installer](https://github.com/pyenv/pyenv-installer)

    ```bash
    curl https://pyenv.run | bash
    ```

- Update pyenv installer

    ```bash
    pyenv update
    ```

- Path Environment
  - Open (or create) the `rc file` for shell.
    - `.bash_profile`
    - `.zshrc`
  - Add NVM Path variables.

    ```rc
    export PATH="$HOME/.pyenv/bin:$PATH"
    command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
    eval (pyenv init -)
    eval "$(pyenv virtualenv-init -)"
    ```

  - Refresh refresh the current window.

    ```bash
    source $HOME/.<rc file>
    ```

- Add pyenv to path and to initialize pyenv/pyenv-virtualenv auto completion

    ```bash
    exec "$SHELL"
    ```

- Check that pyenv is in PATH

    ```bash
    which pyenv
    ```

### [Nx](https://nx.dev/)

- Install Nx CLI

    ```bash
    npm i @nrwl/cli
    ```

### [Firebase CLI](https://firebase.google.com/docs/cli)

- Install

    ```bash
    curl -sL https://firebase.tools | bash
    ```

    or

    ```bash
    npm install -g firebase-tools
    ```

### [fastlane](https://fastlane.tools/)

- Install

    ```bash
    brew install fastlane
    ```

- Setting up fastlane
  - Navigate to your iOS or Android app and run

    ```bash
    fastlane init
    ```

- [Continuous Delivery using fastlane with Flutter](https://docs.flutter.dev/deployment/cd#integrating-fastlane-with-existing-workflows)

### [Python](https://www.python.org/)

- List of Python available versions

    ```bash
    pyenv install --list
    ```

- Install a specific version of python

    ```bash
    pyenv install <python_version>
    ```

- Configure pyenv to use one of these Python versions by default

    ```bash
    pyenv global <python_version>
    ```

- Check that Python is in PATH

    ```bash
    which python
    ```

### [Virtual Environments and pyenv](https://realpython.com/intro-to-pyenv/#virtual-environments-and-pyenv)

- Creating Virtual Environments

    ```bash
    pyenv virtualenv <python_version> <environment_name>
    ```

### [GVM - manage Go versions](https://github.com/moovweb/gvm)

- Install Mercurial

    ```bash
    brew install mercurial
    brew install go
    ```

- Install gvm

    ```bash
    bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
    ```

- Path Environment
  - Open (or create) the `rc file` for shell.
    - `.bash_profile`
    - `.zshrc`
  - Add gvm Path variables.

    ```rc
    [[ -s "/Users/<username>/.gvm/scripts/gvm" ]] && source "/Users/<username>/.gvm/scripts/gvm"
    ```

  - Refresh refresh the current window.

    ```bash
    source $HOME/.<rc file>
    ```

### [Go](https://go.dev/)

- List all installed Go versions

    ```bash
    gvm list
    ```

- List all Go versions available for download

    ```bash
    gvm listall
    ```

- Installing Go

    ```bash
    gvm install <go_version>
    ```

- Automatically set `$GOROOT` and `$GOPATH`

    ```bash
    gvm use <go_version>
    export GOROOT_BOOTSTRAP=$GOROOT
    ```

- Path Environment
  - Open (or create) the `rc file` for shell.
    - `.bash_profile`
    - `.zshrc`
  - Add Go Path variables.

    ```rc
    export GOPATH=$HOME/go
    export GOBIN=$GOPATH/bin
    export PATH=${PATH}:$GOBIN:$GOROOT/bin
    ```

  - Refresh refresh the current window.

    ```bash
    source $HOME/.<rc file>
    ```

## Infrastructure

### [VirtualBox](https://www.virtualbox.org/)

- [Download and Install VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Path Environment](https://www.virtualbox.org/wiki/Mac%20OS%20X%20build%20instructions)
  - Open (or create) the `rc file` for shell.
    - `.bash_profile`
    - `.zshrc`
  - Add VirtualBox Path variables.

    ```rc
    export PATH=/opt/local/bin:/opt/local/sbin:$PATH
    export MANPATH=/opt/local/share/man:$MANPATH
    ```

  - Refresh refresh the current window.

    ```bash
    source $HOME/.<rc file>
    ```

### [Docker](https://www.docker.com/)

- [Install Docker Desktop on Mac](https://docs.docker.com/desktop/install/mac-install/)

### [Kubernetes](https://kubernetes.io/)

- Install
  - Install kubectl binary with curl on macOS

    ```bash
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl"
    ```

  - Install with Homebrew on macOS

    ```bash
    brew install kubectl
    ```

    or

    ```bash
    kubectl version --client
    ```

- Validate the binary (optional)
  - Download the kubectl checksum file

    ```bash
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl.sha256"
    ```

  - Validate the kubectl binary against the checksum file

    ```bash
    echo "$(cat kubectl.sha256)  kubectl" | shasum -a 256 --check
    ```

- Make the kubectl binary executable

    ```bash
    chmod +x ./kubectl
    ```

- Move the kubectl binary to a file location on your system `PATH`

    ```bash
    sudo mv ./kubectl /usr/local/bin/kubectl
    sudo chown root: /usr/local/bin/kubectl
    ```

- Test to ensure the version you installed is up-to-date

    ```bash
    brew install kubernetes-cli
    ```

    or

    ```bash
    kubectl version --client --output=yaml
    ```

- Test to ensure the version you installed is up-to-date

    ```bash
    kubectl cluster-info
    ```

- kubectl configurations
  - The kubectl completion script for Zsh can be generated with the command `kubectl completion zsh`

      ```bash
      source <(kubectl completion zsh)
      ```

  - Upgrade Bash
    - Check Bash's version

        ```bash
        echo $BASH_VERSION
        ```

    - Verify that the desired version is being used

        ```bash
        echo $BASH_VERSION $SHELL
        ```

  - Install bash-completion
    - Install `bash-completion v2`

        ```bash
        brew install bash-completion@2
        ```

    - Add `bash-completion` v2 to `~/.bash_profile`

        ```rc
        export BASH_COMPLETION_COMPAT_DIR="/usr/local/etc/bash_completion.d"
        [[ -r "/usr/local/etc/profile.d/bash_completion.sh" ]] && . "/usr/local/etc/profile.d/bash_completion.sh"
        ```

  - Enable kubectl auto-completion
    - Source the completion script in `~/.bash_profile` file

        ```bash
        echo 'source <(kubectl completion bash)' >>~/.bash_profile
        ```

    - Add the completion script to the /usr/local/etc/bash_completion.d directory

        ```bash
        kubectl completion bash >/usr/local/etc/bash_completion.d/kubectl
        ```

    - If installed `kubectl` with `Homebrew`, then the kubectl completion script should already be in `/usr/local/etc/bash_completion.d/kubectl`. In that case, don't need to do anything.
- kubectl plugins
  - Install `kubectl convert` plugin
    - Download the latest release

      ```bash
      curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl-convert"
      ```

    - Validate the binary
      - Download the kubectl-convert checksum file

          ```bash
          curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl-convert.sha256"
          ```

      - Validate the kubectl-convert binary against the checksum file

          ```bash
          echo "$(cat kubectl-convert.sha256)  kubectl-convert" | shasum -a 256 --check
          ```

    - Make kubectl-convert binary executable

      ```bash
      chmod +x ./kubectl-convert
      ```

    - Move the kubectl-convert binary to a file location on your system `PATH`

      ```bash
      sudo mv ./kubectl-convert /usr/local/bin/kubectl-convert
      sudo chown root: /usr/local/bin/kubectl-convert
      ```

    - Verify plugin is successfully installed

      ```bash
      kubectl convert --help
      ```

### [Microk8s](https://microk8s.io/)

- Install MicroK8s on macOS

    ```bash
    brew install ubuntu/microk8s/microk8s
    microk8s install
    ```

- Check the status while Kubernetes starts

    ```bash
    microk8s status --wait-ready
    ```

- Turn on the services

    ```bash
    microk8s enable dashboard dns registry istio
    ```

- Start using Kubernetes

    ```bash
    microk8s kubectl get all --all-namespaces
    ```

- Access the Kubernetes dashboard

    ```bash
    microk8s dashboard-proxy
    ```

- Start Kubernetes

    ```bash
    microk8s start
    ```

- Stop Kubernetes

    ```bash
    microk8s stop
    ```

### [Helm](https://helm.sh/)

- Install

    ```bash
    brew install helm
    ```

### [Skaffold](https://skaffold.dev/)

- Install

    ```bash
    brew install skaffold
    ```

### [minikube](https://minikube.sigs.k8s.io/docs/)

- Install

    ```bash
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64
    sudo install minikube-darwin-amd64 /usr/local/bin/minikube
    ```

- Start cluster

    ```bash
    minikube start
    ```

- Deploy applications
- Interact with cluster

    ```bash
    kubectl get po -A
    minikube kubectl -- get po -A
    ```

- minikube bundles the Kubernetes Dashboard

    ```bash
    minikube dashboard
    ```

- Pause Kubernetes

    ```bash
    minikube pause
    ```

- Halt the cluster

    ```bash
    minikube stop
    ```

- Delete all of the minikube clusters

    ```bash
    minikube delete --all
    ```

- [Configuration](https://minikube.sigs.k8s.io/docs/handbook/config/)

## IDEs

### [VS Code](https://code.visualstudio.com/)

### [IntelliJ IDEA](https://www.jetbrains.com/idea/)

### [PyCharm](https://www.jetbrains.com/pycharm/)

## API platform

- [Postman](https://www.postman.com/)
