# Oh My Posh PowerShell

Oh My Posh is a custom prompt engine for any shell that has the ability to adjust the prompt string with a function or variable.

**Step 1:**  Open a PowerShell prompt and run the following command

```bash
winget install JanDeDobbeleer.OhMyPosh -s winget
```

**Step 2:** To see the icons displayed in Oh My Posh, install a [Nerd Font](https://www.nerdfonts.com/), and configure your terminal to use it.

**Step 3:** Edit your PowerShell profile script, you can find its location under the `$PROFILE` variable in your preferred PowerShell version.

```bash
notepad $PROFILE
```

When the above command gives an error, make sure to create the profile first.

```bash
New-Item -Path $PROFILE -Type File -Force
```

**Step 4:** In this scenario, it can also be that PowerShell blocks running local scripts. To solve that, set PowerShell to only require remote scripts to be signed using `Set-ExecutionPolicy RemoteSigned`

The Restricted policy doesn't permit any scripts to run. First, check if you have already any Execution Policy activated.

```bash
Get-ExecutionPolicy
```

If you have already an active Execution Policy you can see this. Otherwise, it shows undefined. Now start PowerShell with the **Run as Administrator** option and then use the following command to change the execution policy on the computer to **RemoteSigned.**

```bash
Set-ExecutionPolicy RemoteSigned
```

**Step 5:** Then add the following line to `Documents/PowerShell/Microsoft.PowerShell_profile.ps1`

```bash
oh-my-posh init pwsh --config C:\Users\hossa\AppData\Local\Programs\oh-my-posh\themes\mt.omp.json | Invoke-Expression
```

Run the following command to see available themes:

```bash
Get-PoshThemes
```

Get theme install location

```bash
Get-PoshThemes -List
```

Kali Theme Configuration with custom `name`

```json
{
  "$schema": "https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/schema.json",
  "blocks": [
    {
      "alignment": "left",
      "segments": [
        {
          "foreground": "lightBlue",
          "foreground_templates": ["{{ if .Root }}lightRed{{ end }}"],
          "properties": {
            "display_host": true
          },
          "style": "plain",
          "template": "<{{ if .Root }}lightBlue{{ else }}green{{ end }}>\u250c\u2500\u2500(</>Hossain{{ if .Root }}💀{{ else }}㉿{{ end }}Palin<{{ if .Root }}lightBlue{{ else }}green{{ end }}>)</>",
          "type": "session"
        },
        {
          "foreground": "yellow",
          "properties": {
            "fetch_version": false,
            "fetch_virtual_env": true
          },
          "style": "plain",
          "template": "<{{ if .Root }}lightBlue{{ else }}green{{ end }}>-[</>\ue235 {{ if .Error }}{{ .Error }}{{ else }}{{ if .Venv }}{{ .Venv }}{{ end }}{{ .Full }}{{ end }}<{{ if .Root }}lightBlue{{ else }}green{{ end }}>]</>",
          "type": "python"
        },
        {
          "foreground": "lightWhite",
          "properties": {
            "folder_separator_icon": "<#c0c0c0>/</>",
            "style": "full"
          },
          "style": "plain",
          "template": "<{{ if .Root }}lightBlue{{ else }}green{{ end }}>-[</>{{ .Path }}<{{ if .Root }}lightBlue{{ else }}green{{ end }}>]</>",
          "type": "path"
        },
        {
          "foreground": "white",
          "style": "plain",
          "template": "<{{ if .Root }}lightBlue{{ else }}green{{ end }}>-[</>{{ .HEAD }}<{{ if .Root }}lightBlue{{ else }}green{{ end }}>]</>",
          "type": "git"
        }
      ],
      "type": "prompt"
    },
    {
      "alignment": "right",
      "segments": [
        {
          "foreground": "white",
          "properties": {
            "always_enabled": true,
            "style": "round"
          },
          "style": "plain",
          "template": " {{ .FormattedMs }} ",
          "type": "executiontime"
        },
        {
          "foreground": "green",
          "foreground_templates": ["{{ if gt .Code 0 }}red{{ end }}"],
          "properties": {
            "always_enabled": true
          },
          "style": "plain",
          "template": " {{ if gt .Code 0 }}\uea76{{else}}\uf42e{{ end }} ",
          "type": "status"
        }
      ],
      "type": "prompt"
    },
    {
      "alignment": "left",
      "newline": true,
      "segments": [
        {
          "foreground": "lightBlue",
          "style": "plain",
          "template": "<{{ if .Root }}lightBlue{{ else }}green{{ end }}>\u2514\u2500</>{{ if .Root }}<lightRed>#</>{{ else }}${{ end }} ",
          "type": "text"
        }
      ],
      "type": "prompt"
    }
  ],
  "version": 3
}

```