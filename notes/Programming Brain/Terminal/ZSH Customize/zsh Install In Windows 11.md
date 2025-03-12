# zsh Install In Windows 11

The Z shell is a Unix shell that can be used as an interactive login shell and as a command interpreter for shell scripting. Zsh is an extended Bourne shell with many improvements, including some features of Bash, ksh, and tcsh. Zsh was created by Paul Falstad in 1990 while he was a student at Princeton University.

**Step 1:**  Install Git Bash first, you can download it over [here](https://git-scm.com/downloads). Do installation till Git Bash installed on your PC.

```
https://git-scm.com/downloads
```

**Step 2:** Let’s download latest version of `ZSH` over [here](https://packages.msys2.org/package/zsh?repo=msys&variant=x86_64).

```
https://packages.msys2.org/packages/zsh?repo=msys&variant=x86_64
```

Make sure your file has been downloaded with extension `*.tar.zst*`

Then ekstract file *.*`zst`, i extract it *using [PeaZip](https://peazip.github.io/peazip-64bit.html) you can download it over [here](https://peazip.github.io/peazip-64bit.html).* Extract **`.zst` **file then you will get`.tar` **file and then extract it again from `.tar` file and you will get directory like below.

```
zsh-5.9-2-x86_64.pkg
```

When you open it, you will get `etc` and `usr` directory. For installation `ZSH` you can copy `etc` and `usr` **directory in to `Git Bash`. For Git Bash location maybe you can found it in `C:/Program Files/Git`

Paste `etc` and `usr` **directory in to this location, merge `etc` and `usr` **directory from existing with that will be paste.

**Step 3:**  Once installed, you can verify the installation with the following command. This command will show the currently installed version of zsh.

```bash
zsh --version
```

**Step 4:**  For ZSH running automatically when we open `Git Bash`, we should add a `.bashrc` file at **`C:/Users/user_name/` with this code:

```bash
if [ -t 1 ]; then
exec zsh
fi
```

Oh My Zsh is a delightful, open source, community-driven framework for managing your Zsh configuration. It comes bundled with thousands of helpful functions, helpers, plugins, themes, and a few things that make you shout…

**Step 4:**  Lets install `oh my zsh` with following command

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**Step 5:**  Edit the `~/.zshrc` file, and edit the following line to change the theme. You need at first install theme, in my case i use `oh my posh`

```
C:\Users\User_Name\AppData\Local\Programs\oh-my-posh\themes\kali.omp.json
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