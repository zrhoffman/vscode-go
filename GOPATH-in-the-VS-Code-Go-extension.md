At any point in time, you can run the command `Go: Current GOPATH` to see the GOPATH being used by the extension.

### GOPATH from the environment variable
Out of the box, the extension uses the value of the environment variable `GOPATH`. From Go 1.8 onwards, if no such environment variable is set, then the default GOPATH as deciphered from the command `go env` is used.

### GOPATH from `go.gopath` setting
Setting `go.gopath` in User settings overrides the GOPATH that was derived from the above logic.
Setting `go.gopath` in Workspace settings overrides the one from User settings.
You can set multiple folders as GOPATH in this setting. Note that they should be `;` separated in Windows and `:` separated otherwise.

### GOPATH from `go.inferGopath` setting
Setting `go.inferGopath` overrides the value set in `go.gopath` setting. If `go.inferGopath` is set to true, the extension will try to infer the `GOPATH` from the path of the workspace i.e. the directory opened in `vscode`. It searches upwards in the path for the `src` directory, and sets `GOPATH` to one level above that. It will also include the global GOPATH. Run `go env GOPATH` to find out what your global GOPATH is.

For example, if your project looks like `/aaa/bbb/ccc/src/...`, then opening the directory `/aaa/bbb/ccc/src` (or anything below that) will cause the extension to search upwards, find the `src` component in the path, and set the `GOPATH` to one level above that i.e. `GOPATH=/aaa/bbb/ccc`. 

This setting is useful when you are working on different Go projects which have different GOPATHs. Instead of setting the GOPATH in the workspace settings of each project or setting all the paths as `;`/`:` separated string, you can just set `go.inferGopath` to `true`and the extension uses the right GOPATH automatically.

### GOPATH for installing the Go tools using `go.toolsGopath`
By default, all the dependent Go tools are used from the GOPATH derived from the above logic. If they are available on your PATH, the PATH is used to locate the Go tools. If the Go tools are not in your path, you might end up with the same Go tools installed in each of your GOPATHs. To prevent the Go tools from cluttering your GOPATH, use the `go.toolsGopath` setting to provide a separate location for the Go tools. 

The first time you set `go.toolsGopath`, you will have to run `Go: Install Tools` command so that the Go tools get installed in the provided location.

### GOPATH while debugging

The debug adapter in the Go extension does not have access to your User/Workspace settings. Therefore, the only GOPATH the debugger is aware of is the one set as environment variable outside of VS Code. If there is no such environment variable, then the debugger tries to guess the GOPATH by using the same logic as the `inferGopath` setting described above

You can also provide GOPATH in the `env` property of the debug configuration
Read more on debugging at [Debugging-Go-code-using-VS-Code](https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code)