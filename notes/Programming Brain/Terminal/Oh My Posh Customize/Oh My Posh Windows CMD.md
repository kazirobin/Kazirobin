# Oh My Posh Windows CMD

Oh My Posh is a custom prompt engine for any shell that has the ability to adjust the prompt string with a function or variable.

**Step 1:**  Open a CMD prompt and run the following command

```bash
winget install JanDeDobbeleer.OhMyPosh -s winget
```

**Step 2:** To see the icons displayed in Oh My Posh, install a [Nerd Font](https://www.nerdfonts.com/), and configure your terminal to use it.

**Step 3:** There's no out-of-the-box support for Windows CMD when it comes to custom prompts. There is however a way to do it using [Clink](https://chrisant996.github.io/clink/), which at the same time supercharges your cmd experience. Follow the installation instructions and make sure you select autostart.

Install `Clink` run the following command

```bash
winget search clink
```

Collect the `Id` of the `Clink` and install this

```bash
winget install chrisant996.Clink
```

Integrating `Oh My Posh` with `Clink` is easy: create a new file called `oh-my-posh.lua` in your Clink scripts directory, Find script directory run this command

```bash
clink info
```

And paste the following line

```bash
load(io.popen('oh-my-posh init cmd --config C:/Users/hossa/AppData/Local/Programs/oh-my-posh/themes/kali.omp.json'):read("*a"))()
```