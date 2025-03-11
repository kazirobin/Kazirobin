# Terminal Icons

Terminal-Icons is a PowerShell module that adds file and folder icons that may be missing when displaying files or folders in Windows Terminal, looking up their appropriate icon based on name or extension. It attempts to use icons for well-known files/folders, but falls back to a generic file or folder icon if one is not found.

---

## Setup For PowerShell

**Step 1:**  To install Terminal-Icons with PowerShell, use the command

```bash
Install-Module -Name Terminal-Icons -Repository PSGallery
```

**Step 2:** Then add the following line to `Documents/PowerShell/Microsoft.PowerShell_profile.ps1`

```bash
Import-Module -Name Terminal-Icons
```

**Step 3:**  install starship run the following commands

```bash
winget search starship
winget install starship
```

**Step 4:** Update PowerShell Profile to Use Starship, Open your PowerShell profile in Notepad by running this command

```bash
notepad $PROFILE
```

Add the following line to initialize Starship in PowerShell:

```bash
Invoke-Expression (&starship init powershell)
```

**Step 5:** install `Nerd Fonts` for Icons

Download and install a Nerd Font from [Nerd Fonts](https://www.nerdfonts.com/font-downloads), such as `JetBrainsMono Nerd Font`.

In VS Code, go to `Settings > Terminal` and search for `Integrated: Font Family`. Set the font family to `"JetBrainsMono Nerd Font"` for enhanced icons.