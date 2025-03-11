# Oh My Posh GIT Bash

Oh My Posh is a custom prompt engine for any shell that has the ability to adjust the prompt string with a function or variable.

**Step 1:**  Open a Git Bash and run the following command

```bash
winget install JanDeDobbeleer.OhMyPosh -s winget
```

**Step 2:** Then add the following line to your `~/.bashrc`

```bash
eval "$(oh-my-posh --init --shell bash --config C:/Users/hossa/AppData/Local/Programs/oh-my-posh/themes/kali.omp.json)"
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