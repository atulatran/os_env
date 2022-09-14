# Ubuntu OS Env

============

## Install and config Ubuntu

- [Install Ubuntu 20.04 LTS (Focal Fossa) On UEFI and Legacy BIOS System](https://www.itzgeek.com/post/how-to-install-ubuntu-20-04-lts/)
- Update and Upgrade Ubuntu OS

    ```bash
    sudo apt-get update
    sudo apt-get upgrade -y
    ```

- Change Ubuntu Repository

- Troubleshooting
  - N Skipping acquire of configured file `main/binary-i386/Packages` as repository

    ```bash
    dpkg --print-foreign-architectures
    sudo dpkg --remove-architecture i386
    ```

  - DNS_PROBE_FINISHED_NXDOMAIN in Linux
    - [Ubuntu DNS Error Chrome: DNS_PROBE_FINISHED_NXDOMAIN, Firefox similar](https://askubuntu.com/questions/951057/ubuntu-dns-error-chrome-dns-probe-finished-nxdomain-firefox-similar)
    - Step 1. Open terminal and add below command

        ```bash
        sudo vim /etc/dhcp/dhclient.conf
        ```

    - Step 2. Now add below line in file, and save
      - `supersede domain-name-servers 8.8.8.8;`
    - Step 3. Restart the network

        ```bash
        sudo service network-manager restart
        ```

  - The headphone jack doesn’t (yet) work on NUC 11
    - [Intel NUC 11 with Pop!_OS (Ubuntu) 20.04 LTS](https://benwilcock.wordpress.com/2021/02/17/intel-nuc-11-with-pop_os-ubuntu-20-04-lts/)

        ```bash
        sudo vim /etc/modprobe.d/alsa-base.conf
        ```

    - Add: `options snd-hda-intel model=dell-headset-multi`
    - Reset OS

## VPN

### [OpenVPN 3 Linux](https://community.openvpn.net/openvpn/wiki/OpenVPN3Linux?_ga=2.52596648.1403765179.1641268495-1515907315.1641268495&__cf_chl_jschl_tk__=bx5lIro9p3evsmEZVg5UheeahKY6C31Y6Blahr8nbgA-1641268528-0-gaNycGzNCP0)

- Install

    ```bash
    sudo apt install apt-transport-https
    ```

- Create two files below with root

    ```bash
    sudo vim /etc/apt/trusted.gpg.d/openvpn-repo-pkg-keyring.gpg
    sudo chmod -R a+rwx /etc/apt/trusted.gpg.d/openvpn-repo-pkg-keyring.gpg
    sudo vim /etc/apt/sources.list.d/openvpn3.list
    sudo chmod -R a+rwx /etc/apt/sources.list.d/openvpn3.list
    ```

- Install the OpenVPN repository key used by the OpenVPN 3 Linux packages

    ```bash
    sudo curl -fsSL https://swupdate.openvpn.net/repos/openvpn-repo-pkg-key.pub | gpg --dearmor > /etc/apt/trusted.gpg.d/openvpn-repo-pkg-keyring.gpg
    ```

- Install the proper repository. Replace `$DISTRO` with the release name depending on Debian/Ubuntu distribution

    ```bash
    sudo curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-$DISTRO.list >/etc/apt/sources.list.d/openvpn3.list
    sudo apt-get update
    ```

- Install openvpn3 package

    ```bash
    sudo apt-get install openvpn3 -y
    ```

- Import Key

## FTP client

- FileZila

    ```bash
    sudo apt-get install filezilla -y
    ````

## Public DNS

### Cloudflare Warp

- Reference
  - [Linux desktop client](https://developers.cloudflare.com/warp-client/setting-up/linux)
- Install
  - Package Repository
  - Replace `RELEASE` with the Ubuntu release name (Ubuntu 20.04 => focal)

    ```bash
    sudo apt-get update
    sudo apt-get upgrade
    curl https://pkg.cloudflareclient.com/pubkey.gpg | sudo apt-key add -
    echo 'deb http://pkg.cloudflareclient.com/ <RELEASE> main' | sudo tee /etc/apt/sources.list.d/cloudflare-client.list
    sudo apt update
    ```

  - Install cloudflare-warp package depending on distro

    ```bash
    sudo apt install cloudflare-warp -y
    ```

- Using WARP
  - Initial Connection (To connect for the very first time must call register first)
    - (1) Register the client

        ```bash
        warp-cli register -y
        ```

    - (2) Connect

        ```bash
            warp-cli connect
        ```

    - (3) Verify

        ```bash
        curl <https://www.cloudflare.com/cdn-cgi/trace/>
        ```

- Always stay connected

    ```bash
    warp-cli enable-always-on
    ```

- Switching modes
  - Get a list of the modes to switch

    ```bash
    warp-cli set-mode --help

    ```

    - DNS Only mode via DoH would be accomplished with

        ```bash
        warp-cli set-mode doh
        ```

    - WARP with DoH

        ```bash
        warp-cli set-mode warp+doh
        ```

- Using 1.1.1.1 for Families
  - Families off

    ```bash
        warp-cli set-families-mode off
    ```

    - Malware protection

        ```bash
        warp-cli set-families-mode malware
        ```

    - Malware + Adult Content

        ```bash
        warp-cli set-families-mode full
        ```

- List of all supported commands

    ```bash
    warp-cli --help
    ```

- Feedback
  - Logs required to debug WARP issues

    ```bash
    sudo warp-diag
    ```

    - This will place a `warp-debugging-info.zip` file in the path from which  ran the command.
    - Submit a support ticket (To report bugs or provide feedback to the team)

        ```bash
        sudo warp-diag feedback
        ```

### Google

- [Google Public DNS](https://developers.google.com/speed/public-dns/docs/using)

## Package manager

- [Snapcraft](https://snapcraft.io/)
- [Homebrew](https://docs.brew.sh/)
  - Install

    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

  - Path Environment
    - Open (or create) the `rc file` for shell
      - `.bashrc`
      - `.zshrc`
    - Add Home Path variables

      ```rc
      eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
      ```

    - Refresh refresh the current window

      ```bash
      source $HOME/.<rc file>
      ```

  - Common Packages
    - [curl](https://formulae.brew.sh/formula/curl)
    - [wget](https://formulae.brew.sh/formula/wget)

## Codec

- Install

    ```bash
    sudo apt-get install ubuntu-restricted-extras -y
    ```

## Browsers

- Home page: [Google](https://www.google.com/)
- Extensions:
  - Google Translate
  - Grammarly
- Chrome
- Firefox
  - Firefox not playing videos on Ubuntu 20.04.4 LTS

    ```bash
    sudo apt-get install ffmpeg -y
    ```

- Brave
- Tor

## Manage Files

- [Beyond Compare](https://www.scootersoftware.com/)
  - [Crack Beyond Compare](https://www.jianshu.com/p/93303b9fb21a)
  - Install

    ```bash
    wget https://www.scootersoftware.com/bcompare-4.4.0.25886_amd64.deb
    sudo apt-get update
    sudo apt-get install gdebi-core
    sudo gdebi bcompare-4.4.0.25886_amd64.deb
    ```

  - Crack
    - [Crack permanent use](https://www.jianshu.com/p/93303b9fb21a)

        ```bash
        cd /usr/lib/beyondcompare/
        sudo sed -i "s/keexjEP3t4Mue23hrnuPtY4TdcsqNiJL-5174TsUdLmJSIXKfG2NGPwBL6vnRPddT7tH29qpkneX63DO9ECSPE9rzY1zhThHERg8lHM9IBFT+rVuiY823aQJuqzxCKIE1bcDqM4wgW01FH6oCBP1G4ub01xmb4BGSUG6ZrjxWHJyNLyIlGvOhoY2HAYzEtzYGwxFZn2JZ66o4RONkXjX0DF9EzsdUef3UAS+JQ+fCYReLawdjEe6tXCv88GKaaPKWxCeaUL9PejICQgRQOLGOZtZQkLgAelrOtehxz5ANOOqCaJgy2mJLQVLM5SJ9Dli909c5ybvEhVmIC0dc9dWH+/N9KmiLVlKMU7RJqnE+WXEEPI1SgglmfmLc1yVH7dqBb9ehOoKG9UE+HAE1YvH1XX2XVGeEqYUY-Tsk7YBTz0WpSpoYyPgx6Iki5KLtQ5G-aKP9eysnkuOAkrvHU8bLbGtZteGwJarev03PhfCioJL4OSqsmQGEvDbHFEbNl1qJtdwEriR+VNZts9vNNLk7UGfeNwIiqpxjk4Mn09nmSd8FhM4ifvcaIbNCRoMPGl6KU12iseSe+w+1kFsLhX+OhQM8WXcWV10cGqBzQE9OqOLUcg9n0krrR3KrohstS9smTwEx9olyLYppvC0p5i7dAx2deWvM1ZxKNs0BvcXGukR+/g" BCompare
        ```

    - Key

        ```txt
        --- BEGIN LICENSE KEY ---
        GXN1eh9FbDiX1ACdd7XKMV7hL7x0ClBJLUJ-zFfKofjaj2yxE53xauIfkqZ8FoLpcZ0Ux6McTyNmODDSvSIHLYhg1QkTxjCeSCk6ARz0ABJcnUmd3dZYJNWFyJun14rmGByRnVPL49QH+Rs0kjRGKCB-cb8IT4Gf0Ue9WMQ1A6t31MO9jmjoYUeoUmbeAQSofvuK8GN1rLRv7WXfUJ0uyvYlGLqzq1ZoJAJDyo0Kdr4ThF-IXcv2cxVyWVW1SaMq8GFosDEGThnY7C-SgNXW30jqAOgiRjKKRX9RuNeDMFqgP2cuf0NMvyMrMScnM1ZyiAaJJtzbxqN5hZOMClUTE+++
        --- END LICENSE KEY -----
        ```

## Offices

- Microsoft Offices (Word, Excel, ...)
- Libre Offices
- Unikey
- IBus-Bamboo
  - Install

    ```bash
    sudo add-apt-repository ppa:bamboo-engine/ibus-bamboo
    sudo apt-get update
    sudo apt-get install ibus-bamboo
    ibus restart
    ```

  - Setting
- PDF - Xournal

    ```bash
    sudo apt-get install xournal -y
    ```

## Manage Windows

- [Spectacle](https://www.spectacleapp.com/)

## Screenshot

- [Flameshot](https://flameshot.org/)
  - Install

    ```bash
    sudo snap install flameshot
    ```

  - Configuration - Save Path

## Terminals

- xclip
  - Install

    ```bash
    sudo apt-get install xclip
    ```

- curl
  - Install

    ```bash
    sudo apt-get install curl
    ```

- [tmux](https://github.com/tmux/tmux/wiki)
  - Install

    ```bash
    brew install tmux
    ```

- [Vim](https://github.com/vim/vim)
  - Install

    ```bash
    brew install vim
    ```

    or

    ```bash
    sudo apt-get install vim -y
    ```

- [Zsh](https://www.zsh.org/)
  - [Installing ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

    ```bash
    brew install zsh
    ```

    or

    ```bash
    sudo apt-get install zsh -y
    ```

- [Oh My ZSH](https://ohmyz.sh/)
  - Install

    ```bash
    brew install zsh
    ```

    or

    ```bash
    sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```

## Teamworks

- [Slack](https://slack.com/)

    ```bash
    sudo snap install slack --classic
    ```

- Microsoft Teams
  - Microsoft Teams - Preview

    ```bash
        sudo snap install teams
    ```

  - Microsoft Teams - Insiders

    ```bash
        sudo snap install teams-insiders
    ```

## Video Meetings

- [Zoom](https://zoom.us/)

    ```bash
    sudo snap install zoom-client
    ```

- [Meet](https://meet.google.com/)

## Version Control System

- [Git](https://git-scm.com/)
  - Install

    ```bash
    sudo apt-get install git -y
    ```

  - Config

    ```bash
    git config --global user.name "username"
    git config --global user.email "email"
    ```

  - Large File Storage
    - References
      - [Installing Git Large File Storage](https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage)
      - [Git extension for versioning large files](https://git-lfs.github.com/)
      - Config

        ```bash
        curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
        sudo apt-get install git-lfs -y
        git lfs install
        git lfs push --all origin
        git lfs track "*.m4a"
        git add .gitattributes
        git lfs migrate import --include="*.m4a"
        ```

  - SSH
    - Generating a new SSH key

        ```bash
        ssh-keygen -t ed25519 -C "your_email@example.com"
        ```

    - Adding SSH key to the ssh-agent

        ```bash
        eval "$(ssh-agent -s)"
        ssh-add ~/.ssh/id_ed25519
        ```

    - Checked for existing SSH keys

        ```bash
        ls -al ~/.ssh
        ```

    - Copy the SSH public key to clipboard

        ```bash
        cat ~/.ssh/id_ed25519.pub
        ```

    - Add the SSH key to account on GitHub, Gitlab
  - [Using Multiple SSH Keys for Multiple GitHub Accounts](https://www.section.io/engineering-education/using-multiple-ssh-keys-for-multiple-github-accounts/)
  - [git-flow](https://danielkummer.github.io/git-flow-cheatsheet/)
- [Sourcetree](https://www.sourcetreeapp.com/)
- [GitKraken](https://www.gitkraken.com/)
- [SmartGit](https://www.syntevo.com/smartgit/)

## SDKs

### [Software Development Kit](https://sdkman.io/)

- [Installation SDKMAN](https://sdkman.io/install)

    ```bash
    curl -s "https://get.sdkman.io" | bash
    source "$HOME/.sdkman/bin/sdkman-init.sh"
    ```

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

### [Flutter SDK](https://docs.flutter.dev/get-started/install/linux)

- Install

    ```bash
    sudo snap install flutter --classic
    ```

- Path Environment
  - Determine the path of clone of the Flutter SDK.
  - Open (or create) the `rc file` for shell
    - `.bashrc`
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

- Install use the Homebrew package manager

    ```bash
    brew tap leoafarias/fvm
    brew install fvm
    ```

- Install as a pub package

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

### Managing Dart projects with multiple packages

- Reference
  - [Melos](https://melos.invertase.dev/)
  - [Managing multi-package Flutter projects with Melos](https://medium.com/flutter-community/managing-multi-package-flutter-projects-with-melos-c8ce96fa7c82)
- Install

    ```bash
    dart pub global activate melos
    ```

### Flutter Stylizer

- Reference
  - [gmlewis/go-flutter-stylizer](https://github.com/gmlewis/go-flutter-stylizer)
  - [gmlewis/flutter-stylizer](https://github.com/gmlewis/flutter-stylizer)

### [Android Setup](https://docs.flutter.dev/get-started/install/linux#android-setup)

- Download and install Android Studio.
- Installs the latest Android SDK, Android SDK Command-line Tools, and Android SDK Build-Tools.
- Set the directory that Android Studio is installed.

    ```bash
    flutter config --android-studio-dir <directory>
    flutter config --android-sdk <directory>
    ```

    ```bash
    flutter config --android-studio-dir=/snap/android-studio/current/android-studio
    flutter config --android-sdk /home/<username>/snap/android-sdk
    ```

- Set up the Android emulator.
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

### [Python Version Management - pyenv](https://github.com/pyenv/pyenv)

- References
  - [Managing Multiple Python Versions With pyenv](https://realpython.com/intro-to-pyenv/)
  - [Python Versions Management With pyenv](https://switowski.com/blog/pyenv)
  - [Simple Python Version Management: pyenv](https://github.com/pyenv/pyenv)
  - [How to Manage Multiple Python Versions in MacOS. (2021 Guide)](https://chamikakasun.medium.com/how-to-manage-multiple-python-versions-in-macos-2021-guide-f86ef81095a6)
  - [Installing pyenv on macOS](https://binx.io/2019/04/12/installing-pyenv-on-macos/)
- [Install the build dependencies](https://github.com/pyenv/pyenv/wiki)

    ```bash
    sudo apt-get install -y make build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
    libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl
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

- Install `bison`

  ```bash
  sudo apt-get install curl git mercurial make binutils bison gcc build-essential -y
  ```

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

- Install

    ```bash
    sudo apt install virtualbox virtualbox-ext-pack
    ```

- [Path Environment](https://www.virtualbox.org/wiki/Linux_Downloads)
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

- [Install Docker Desktop on Linux](https://docs.docker.com/desktop/install/linux-install/)

    ```bash
    sudo snap install docker
    ```

- Running Docker as normal user

    ```bash
    sudo addgroup --system docker
    sudo adduser $USER docker
    newgrp docker
    sudo snap disable docker
    sudo snap enable docker
    ```

### [Docker Compose](https://docs.docker.com/compose/install/)

- Install

    ```bash
    sudo curl -L "https://github.com/docker/compose/releases/download/v1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    docker-compose --version
    ```

### [Kubernetes](https://kubernetes.io/)

- Install
  - Install

    ```bash
    sudo snap install kubectl --classic
    ```

  - Install with Homebrew

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

- Install

    ```bash
    sudo snap install microk8s --classic
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

    or

    ```bash
    sudo snap install helm --classic
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

    or

    ```bash
    wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    ```

- Copy the downloaded file and store it into the /usr/local/bin/minikube directory

    ```bash
    sudo cp minikube-linux-amd64 /usr/local/bin/minikube
    ```

- Give the file executive permission

    ```bash
    sudo chmod 755 /usr/local/bin/minikube
    ```

- Verify have successfully installed Minikube by checking the version of the software

    ```bash
    minikube version
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
- Managing kubernetes with Minikube
  - Common Minikube Commands
    - Show the kubectl configuration

        ```bash
        kubectl config view
        ```

    - Show the cluster information

        ```bash
        kubectl cluster-info
        ```

    - Check running nodes

        ```bash
        kubectl get nodes
        ```

    - Show a list of all the Minikube pods

        ```bash
        kubectl get pod
        ```

    - SSH into the Minikube VM

        ```bash
        minikube ssh
        ```

    - Stop running the single node cluster type

        ```bash
        minikube stop
        ```

    - Check its status use

    ```bash
        minikube status
      ```

  - Delete the single node cluster

    ```bash
    minikube delete
    ```

  - Show a list of installed Minikube add-ons

    ```bash
    minikube addons list
    ```

- Access Minikube Dashboard
  - Minikube comes with a dashboard add-on by default.
  - The web dashboard provides a way to manage Kubernetes cluster without actually running commands in the terminal.
  - To enable and access the Minikube dashboard via terminal

    ```bash
    minikube dashboard
    ```

  - Once exit the terminal, the process will end and the Minikube dashboard will shut down.
  - Alternatively, can access the dashboard directly via browser
  - To do so, acquire the dashboard’s IP address

    ```bash
    minikube dashboard --url
    ```

  - Access Minikube dashboard by browsing to dashboard’s IP address.
- [virtualbox | minikube](https://minikube.sigs.k8s.io/docs/drivers/virtualbox/)
  - Start a cluster using the virtualbox driver
  
    ```bash
    minikube start --driver=virtualbox
    ```

  - Make virtualbox the default driver:

    ```bash
    minikube config set driver virtualbox
    ```

  - Troubleshooting: debug crashes

    ```bash
    minikube start --alsologtostderr -v=7
    ```

  - [Minikube on Ubuntu - Could Not Read CA certificate](http://computerbryan.com/minikube-on-ubuntu.html)
    - Open

        ```bash
        sudo vim /var/lib/snapd/apparmor/profiles/snap.docker.docker
        ```

    - Add

    ```rc
    owner @{HOME}/.minikube/certs/*
    ```

    - Minikube login docker

        ```bash
        eval $(minikube docker-env)
        ```

    - Run AppArmor

        ```bash
        sudo apparmor_parser -r /var/lib/snapd/apparmor/profiles/snap.docker.docker
        ```

## IDEs

### [VS Code](https://code.visualstudio.com/)

- Install

    ```bash
    sudo snap install code --classic
    ```

- Extensions

### [Android Studio](https://developer.android.com/studio?gclid=Cj0KCQjw94WZBhDtARIsAKxWG-_CqYkUJe5yTX-W3xQI9uG1UMQqLDllh7M0I5m8SpC5eVOgeF52xfkaAhWgEALw_wcB&gclsrc=aw.ds)

- Install

    ```bash
    sudo snap install android-studio --classic
    ```

- Update plugin - `Kotlin`
- Android Studio Setup
- Install Android SDK
- Create Android Virtual Device
- Plugins

### [IntelliJ IDEA](https://www.jetbrains.com/idea/)

- IntelliJ IDEA Community

    ```bash
    sudo snap install intellij-idea-community --classic
    ```

- IntelliJ IDEA Ultimate

    ```bash
    sudo snap install intellij-idea-ultimate --classic
    ```

### [PyCharm](https://www.jetbrains.com/pycharm/)

- Pycharm Community

    ```bash
    sudo snap install pycharm-community --classic
    ```

- Pycharm Professional

    ```bash
    sudo snap install pycharm-professional --classic
    ```

## API platform

- [Postman](https://www.postman.com/)
