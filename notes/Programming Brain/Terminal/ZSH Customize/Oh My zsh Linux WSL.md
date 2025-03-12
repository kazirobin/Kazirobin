# Oh My zsh Linux/WSL

The Z shell is a Unix shell that can be used as an interactive login shell and as a command interpreter for shell scripting. Zsh is an extended Bourne shell with many improvements, including some features of Bash, ksh, and tcsh. Zsh was created by Paul Falstad in 1990 while he was a student at Princeton University.

**Step 1:**  Install ZSH with following command

```bash
sudo apt install zsh
```

**Step 2:**  Once installed, you can verify the installation with the following command. This command will show the currently installed version of zsh.

```bash
zsh --version
```

**Step 3:**  To make zsh the default shell on your Linux system, use the following command. Enter the root password when prompted.

```bash
chsh -s /usr/bin/zsh
```

Oh My Zsh is a delightful, open source, community-driven framework for managing your Zsh configuration. It comes bundled with thousands of helpful functions, helpers, plugins, themes, and a few things that make you shout…

**Step 4:**  Lets install `oh my zsh` with following command

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**Step 5:**  Edit the `~/.zshrc` file, and edit the following line to change the theme.

```bash
ZSH_THEME="agnoster"
```

**Step 6:**  To use the agnoster theme you have to install some fonts.

```bash
sudo apt install fonts-powerline
```

## Install PowerLevel10k on WSL

Powerlevel10k is a theme for Zsh. It emphasizes speed, flexibility and out-of-the-box experience.

**Step 1:**  Installation of PowerLevel10k for Oh My Zsh

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

**Step 2:**  Now, edit the ZSH_THEME in ~/.zshrc file and restart the Ubuntu app. You will be prompted with the configuration wizard for PowerLevel10k. If not, type p10k configure if the configuration wizard doesn't start automatically.

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

## Install Autosuggestions & Syntax Highlighting

**Step 1:**  Download zsh-autosuggestions

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

**Step 2:**  Download zsh-syntax-higlighting

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

**Step 3:**  Edit `~/.zshrc` file, find `plugins=(git)` replace with the following line.

```bash
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```