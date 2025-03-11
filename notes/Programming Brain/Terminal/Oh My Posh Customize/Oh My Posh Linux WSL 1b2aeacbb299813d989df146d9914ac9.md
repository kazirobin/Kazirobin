# Oh My Posh Linux/WSL

Oh My Posh is a custom prompt engine for any shell that has the ability to adjust the prompt string with a function or variable.

**Step 1:**  Open the Linux/WSL terminal and run the following command

```bash
curl -s https://ohmyposh.dev/install.sh | bash -s
```

By default the script will install to `~/bin` or `~/.local/bin` depending on which one exists, or the existing Oh My Posh executable's installation folder. If you want to install to a different location you can specify it using the `-d` flag:

```bash
curl -s https://ohmyposh.dev/install.sh | bash -s -- -d ~/bin
```

Now that Oh My Posh is installed, you can go ahead and configure your terminal and shell to get the prompt to look exactly like you want.

**Step 2:** To see the icons displayed in Oh My Posh, install a [Nerd Font](https://www.nerdfonts.com/), and configure your terminal to use it. Oh My Posh was designed to use Nerd Fonts. Nerd Fonts are popular fonts that are patched to include icons. To see the icons displayed in Oh My Posh, **install** a Nerd Font, and **configure** your terminal to use it.

Oh My Posh has a CLI to help you select and install a Nerd Font and configure your terminal to use it.

```bash
oh-my-posh font install
```

Once installed, you can verify the installation by running the following line

```bash
which oh-my-posh
```

Ensure the `oh-my-posh` binary is available in your `PATH`. If you've installed `oh-my-posh` to a non-standard location, you may need to add its location to your `PATH` by modifying your `.bashrc`:

```bash
**export PATH=$PATH:/home/{user}/.local/bin**
```

**Step 3:** Add the following snippet as the last line to `~/.bashrc` and find the theme directory with the `find` command like this `find ~ -type f -name "*.omp.json”`

```bash
eval "$(oh-my-posh init bash --config ~/.cache/oh-my-posh/themes/kali.omp.json)"
```

Once added, reload your profile for the changes to take effect.

```bash
exec bash
# or
source ~/.bashrc
```

## For Easy Installation

oh my posh can also be installed manually by downloading the release. Depending on your distro

```bash
sudo wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh
sudo chmod +x /usr/local/bin/oh-my-posh
```

Get a theme for Oh My Posh

```bash
mkdir ~/.poshthemes
wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -O ~/.poshthemes/themes.zip
unzip ~/.poshthemes/themes.zip -d ~/.poshthemes
chmod u+rw ~/.poshthemes/*.json
```

To see the icons displayed in Oh My Posh, install a [Nerd Font](https://www.nerdfonts.com/), and configure your terminal to use it. Oh My Posh was designed to use Nerd Fonts. Nerd Fonts are popular fonts that are patched to include icons. To see the icons displayed in Oh My Posh, **install** a Nerd Font, and **configure** your terminal to use it.

Oh My Posh has a CLI to help you select and install a Nerd Font and configure your terminal to use it.

```bash
oh-my-posh font install
```

Add the following snippet as the last line to `~/.bashrc`

```bash
eval "$(oh-my-posh init bash --config ~/.poshthemes/kali.omp.json)"
```

Save and reload the Bash configuration

```bash
source ~/.bashrc
```