# ESP32 & Espressif IDF In VS Code on Windows

Notes on getting Espressif IDF and the IDF console working in VS Code.

### User settings.json config

VS Code console profile settings have changed. First we need to define our Windows console profiles, notice we will make our own console specifically for the Espressif IDF, labeled here "as ESP32 CMD"

We want to steal the arguments from the shortcut. In my case for IDF Version 4.4

`"C:/Espressif/idf_cmd_init.bat esp-idf-e91d384503485fbb54f6ce3d11e841fe"`

Remember VS Code respects forward slashes.

This will launch a 

```
    "terminal.integrated.defaultProfile.windows": "PowerShell",
    "terminal.integrated.profiles.windows": {
        "PowerShell": {
            "source": "PowerShell",
            "icon": "terminal-powershell"
        },
        "Command Prompt": {
            "path": [
                "${env:windir}\\Sysnative\\cmd.exe",
                "${env:windir}\\System32\\cmd.exe"
            ],
            "args": [],
            "icon": "terminal-cmd"
        },
        "ESP32 CMD": {
            "path": [
                "${env:windir}\\Sysnative\\cmd.exe",
                "${env:windir}\\System32\\cmd.exe"
            ],
            "args": [
                "/k",
                "C:/Espressif/idf_cmd_init.bat esp-idf-e91d384503485fbb54f6ce3d11e841fe"
            ],
            "icon": "terminal-cmd"
        },
        "Git Bash": {
            "source": "Git Bash"
        }
```

Now we can load our IDF console by default in our project workspace.

### Workspace settings for loading our IDF CMD by default

```
	"settings": 
	{
		"terminal.integrated.defaultProfile.windows": "ESP32 CMD"
	}
```

### Make sure to add your IDF folder to the include path for C/C++ extensions.

```
            "includePath": [
                "${workspaceFolder}/**",
                "C:/Espressif/frameworks/esp-idf-v4.4.2/**"
                ]
```

