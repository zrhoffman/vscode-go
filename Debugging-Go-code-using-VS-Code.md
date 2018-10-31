## Install delve

You can manually install delve as per the [Installation Instructions](https://github.com/derekparker/delve/tree/master/Documentation/installation).

Based on how you install delve it will either end up in your `PATH` or `GOPATH/bin`. 
If `dlv` binary is in your `GOPATH/bin` and this GOPATH is not set as an environment variable, then make sure your PATH points to this `GOPATH/bin` so that the Go extension can find the `dlv` binary.

## Set up configurations in your settings

The below settings are used by the debugger
- `go.gopath`. See [GOPATH in VS Code](https://github.com/Microsoft/vscode-go/wiki/GOPATH-in-the-VS-Code-Go-extension)
- `go.inferGopath`. See [GOPATH in VS Code](https://github.com/Microsoft/vscode-go/wiki/GOPATH-in-the-VS-Code-Go-extension)
- `go.delveConfig`
     - `apiVersion`: Controls the version of delve apis to be used when launching the delve headless server. Default is 2.
     - `dlvLoadConfig`: Not applicable when `apiVersion` is 1. The configuration passed to delve. Controls [various features of delve](https://github.com/Microsoft/vscode-go/blob/0.6.85/package.json#L431-L468) that affects the variables shown in the debug pane.
         - `maxStringLen`:  maximum number of bytes read from a string
         - `maxArrayValues`:  maximum number of elements read from an array, a slice or a map
         - `maxStructFields`:  maximum number of fields read from a struct, -1 will read all fields
         - `maxVariableRecurse`:  how far to recurse when evaluating nested types
         - `followPointers`:  requests pointers to be automatically dereferenced         
     

Some common cases where you might want to tweak the configurations passed to delve
- Change the default cap of 64 on string and array length when inspecting variables in the debug viewlet.
- Evaluate variables that are nested when inspecting them in the debug viewlet.

## Set up configurations in launch.json

Once delve is installed and is available in your $PATH, run the command `Debug: Open launch.json`. If you didnt already have a launch.json file, this will create one with the below default configuration.

```json
{
	"version": "0.2.0",
	"configurations": [
		{
			"name": "Launch",
			"type": "go",
			"request": "launch",
			"mode": "auto",
			"program": "${fileDirname}",
			"env": {},
			"args": []
		}
	]
}
```

The `program` option is mandatory and takes path to a folder or file.

* This can refer to a package folder to debug, or a file within that folder. 
* This should be a full path and not relative.
* Use `${workspaceFolder}` to debug package at the root of the workspace that is opened in VS Code 
* Use `${file}` to debug the current file.
* Use `${fileDirname}` to debug the package to which the current file belongs to.

The `mode` parameter can be set to:

* `debug` to compile the contents of the program folder and launch under the debugger. [default]
* `test` to debug tests in the program folder. To debug a single test, pass `-test.run` and the Test name as args. Additionally, you can pass `-test.v` to get verbose output as well.
* `auto` to automatically detect whether to use `debug` or `test` based in the current file that is open.
* `exec` to run a pre-built binary specified in program, for example `"program":"${workspaceRoot}/mybin"`.
* `remote` to attach to a remote headless Delve server.  You must manually run Delve on the remote machine, and provide the additional `remotePath`, `host` and `port` debug configuration options pointing at the remote machine.

If your build needs build tags (e.g. `go build -tags whatever_tag`), then add the parameter `buildFlags` with the content `"-tags whatever_tag"`.  Multiple tags are supported, by *enclosing them in single quotes within the double quotes* like so: `"-tags 'first_tag second_tag third_tag'"`.

In version 0.6.66 or lesser of the Go extension, the debugger cannot read your settings. It figures out the GOPATH from either the environment variables or from the path provided in the `program` option. If you have set multiple GOPATHs in the `go.gopath` setting, pass the same in the `env` option of the `launch.json` as an environment variable.

As of 0.6.67 version, the debugger will inherit the GOPATH from settings. Run `Go: Current GOPATH` command to see the GOPATH being used by the Go extension and the debugger.

## Snippets for Debug Configurations

As of 0.6.54 version of the Go extension, you can now make use of snippets while editing the launch.json file. 
Type "Go" and you will get debug configuration snippets for debugging current file/package, a test function etc.

## Debugging the Debugger?

Set `showLog` attribute in your debug configuration to `true`. You will see logs in the debug console from delve.

Set `trace` attribute in your debug configuration to `verbose`. You will see logs in the debug console from the Go extension's debug adapter. These logs will be saved to a file whose path will be printed at the beginning in the debug console.

If you want to dig deeper and debug the debugger using source code of this extension, read [building-and-debugging-the-extension](https://github.com/Microsoft/vscode-go/wiki/Building,-Debugging-and-Sideloading-the-extension-in-Visual-Studio-Code#building-and-debugging-the-extension)

## Remote Debugging

To remote debug using VS Code, you must first run a headless Delve server on the target machine.  For example:

```bash
$ dlv debug --headless --listen=:2345 --log
```

Any arguments that you want to pass to the program you are debugging must be passed to this Delve server that runs on the target machine. For example:

```bash
$ dlv debug --headless --listen=:2345 --log -- -myArg=123
```

> Note: Do not pass the flag `–api-version=2` to dlv. The Go extension doesn't support v2 of delve APIs yet.

Then, create a remote debug configuration in VS Code `launch.json`.

```json
{
	"name": "Remote",
	"type": "go",
	"request": "launch",
	"mode": "remote",
	"remotePath": "${workspaceRoot}",
	"port": 2345,
	"host": "127.0.0.1",
	"program": "${workspaceRoot}",
	"env": {}
}
```

> Note: `remotePath` must be correct otherwise breakpoints will silently fail

When you launch the debugger with this new `Remote` target selected, VS Code will send debugging
commands to the `dlv` server you started previously instead of launching it's own `dlv` instance against your app.

The above example runs both the headless `dlv` server and the VS Code debugger locally on the same machine.  For an
example of running these on different hosts, see the example of debugging a process running in a docker host at https://github.com/lukehoban/webapp-go/tree/debugging.

## Troubleshooting

### Cannot find Delve debugger at ... Ensure it is in your "GOPATH/bin" or "PATH".

Like the error message says, the extension cannot find `dlv`. Remember, the debug adapter cannot read the VS Code settings.

**_Solution_**: Add the location where dlv is installed to your PATH. You can find this location by running `which dlv` or `where dlv`

### Cannot find package ".." in any of ... 

The debugger is not using the right GOPATH. This shouldn't happen, if it does, log a bug. 

**_Solution_**: Until the bug you logged is resolved, the work around is to add the GOPATH as an env var in the `env` property in the `launch.json` file.

### Failed to continue: "Error: spawn EACCES"

You have `dlv` running just fine from command line, but VS Code gives this access related error. 
This can happen if the extension is trying to run the `dlv` binary from a wrong location.
The Go extension first tries to find `dlv` in your $GOPATH/bin and then in your $PATH.  

**_Solution_**: Run `which dlv` in the command line. If this doesn't match your `GOPATH/bin`, then delete the `dlv` file in 
your `GOPATH/bin`


### could not launch process: stat ***/debug.test: no such file or directory

You may see this in the debug console, while trying to run in the `test` mode. This happens when the `program` attribute points to a folder with no test files.

**_Solution_**: Ensure that the `program` attribute points to the folder that contains the test files you want to run.

### could not launch process: could not fork/exec

#### OSX ####

This usually happens in OSX due to signing issues. See the discussions in please see [#717](https://github.com/Microsoft/vscode-go/issues/717), [#269](https://github.com/Microsoft/vscode-go/issues/269) and [derekparker/delve/357](https://github.com/derekparker/delve/issues/357)

**_Solution_**: You may have to uninstall dlv and install it manually as per [instructions](https://github.com/derekparker/delve/blob/master/Documentation/installation/osx/install.md#manual-install)

#### Linux/Docker ####

Docker has security settings preventing ptrace(2) operations by default within the container.

**_Solution_**: To run your container insecurely, pass `--security-opt=seccomp:unconfined` to docker run when starting. Reference: [derekparker/delve/515](https://github.com/derekparker/delve/issues/515)

### could not launch process: exec: "lldb-server": executable file not found in $PATH

This error can show up for Mac users using delve of version 0.12.2 or above. Not sure why, but doing a `xcode-select --install` has solved the problem for users who have seen this issue.

### Unverified breakpoints when remote debugging

Check the version of delve api being used in the remote delve process. v2 is not yet supported in the Go extension. So if you have `–api-version=2` being passed to `dlv`, remove that flag and try again