## How do I start the test suite using a keyboard shortcut?

1. Edit your keybindings.json file:  `Code > Preferences > Keyboard Shortcuts`
2. Add a new entry such as:

```
	{
		"key": "cmd+r",
		"command": "go.test.package"
	}
```

The list of available Go specific commands is available in [this file](https://github.com/Microsoft/vscode-go/blob/master/package.json).

3. Click `cmd + r` to start the package test suite.