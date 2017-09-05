## Install delve

If you are on Windows or Linux, running `Go: Install/Update Tools` would have installed delve for you.
If you don't want to run that command or you are on OS X, you can manually install delve as per the [Installation Instructions](https://github.com/derekparker/delve/tree/master/Documentation/installation).
On OS X it requires creating a self-signed cert to sign the `dlv` binary.

Based on how you install delve it will either end up in your `PATH` or `GOPATH/bin`. 
If `dlv` binary is in your `GOPATH/bin` and this GOPATH is not set as an environment variable, then make sure your PATH points to this `GOPATH/bin` so that the Go extension can find the `dlv` binary.

## Set up configurations in launch.json

Once delve is installed, you can either press `F5` or go to the Code debug viewlet and select the configuration gear. If you are using Visual Studio Code 1.8.1 or below, you will see a pop up asking you to select your environment. Select 'Go'. 

You will now see a `launch.json` file created for your workspace, which will contain the configurations for debugging. By default, there would be a single configuration as below:

```json
{
	"version": "0.2.0",
	"configurations": [
		{
			"name": "Launch",
			"type": "go",
			"request": "launch",
			"mode": "debug",
			"remotePath": "",
			"port": 2345,
			"host": "127.0.0.1",
			"program": "${workspaceRoot}",
			"env": {},
			"args": [],
			"showLog": true
		}
	]
}
```

The `program` option is mandatory and can refer to a package folder to debug, or a file within that folder. This should be a full path and not relative.

The `mode` parameter can be set to:

* `debug` to compile the contents of the program folder and launch under the debugger. [default]
* `test` to debug tests in the program folder. To debug a single test, pass `-test.run` and the Test name as args.
* `exec` to run a pre-built binary specified in program, for example `"program":"${workspaceRoot}/mybin"`.
* `remote` to attach to a remote headless Delve server.  You must manually run Delve on the remote machine, and provide the additional `remotePath`, `host` and `port` debug configuration options pointing at the remote machine.

The debugger cannot read your settings. It figures out the GOPATH from either the environment variables or based on the path provided in the `program` option. If you have set multiple GOPATHs in the `go.gopath` setting, pass the same in the `env` option of the `launch.json` as an environment variable.

## Snippets for Debug Configurations

As of 0.6.54 version of the Go extension, you can now make use of snippets while editing the launch.json file. 
Type "Go" and you will get debug configuration snippets for debugging current file/package, a test function etc.

## Debugging the Debugger?

Set `showLog` attribute in your debug configuration to `true`. You will see logs in the debug console from delve.

Set `trace` attribute in your debug configuration to `verbose`. You will see logs in the debug console from the Go extension's debug adapter. These logs will be saved to a file whose path will be printed at the beginning in the debug console.

## Remote Debugging

To remote debug using VS Code, you must first run a headless Delve server on the target machine.  For example:

```bash
$ dlv debug --headless --listen=:2345 --log
```

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
	"env": {},
	"args": []
}
```

When you launch the debugger with this new `Remote` target selected, VS Code will send debugging
commands to the `dlv` server you started previously instead of launching it's own `dlv` instance against your app.

The above example runs both the headless `dlv` server and the VS Code debugger locally on the same machine.  For an
example of running these on different hosts, see the example of debugging a process running in a docker host at https://github.com/lukehoban/webapp-go/tree/debugging.

## Troubleshooting

### Cannot find Delve debugger at ... Ensure it is in your "GOPATH/bin" or "PATH".

Like the error message says, the extension cannot find `dlv`. 
This can happen if `dlv` got installed to your GOPATH which you have set using `go.gopath` in the settings.
Since the debug adapter cannot read the settings, it is not aware of this GOPATH.

**_Solution_**: You can either set the GOPATH as an env var outside VS Code or point PATH to the dlv binary.
Another way is to update the `env` property in `launch.json` to have GOPATH as a env variable.

### Cannot find package ".." in any of ... 

If you have set GOPATH using `go.gopath` in your settings, then the debug adapter cannot read it as the it is not aware of the settings. 

**_Solution_**: Add the GOPATH as an env var in the `env` property in the `launch.json` file.

### Failed to continue: "Error: spawn EACCES"

You have `dlv` running just fine from command line, but VS Code gives this access related error. 
This can happen if the extension is trying to run the `dlv` binary from a wrong location.
The Go extension first tries to find `dlv` in your $GOPATH/bin and then in your $PATH.  

**_Solution_**: Run `which dlv` in the command line. If this doesnt match your `GOPATH/bin`, then delete the `dlv` file in 
your `GOPATH/bin`


### could not launch process: stat ***/debug.test: no such file or directory

You may see this in the debug console, while trying to run in the `test` mode. This happens when the `program` attribute points to a folder with no test files.

**_Solution_**: Ensure that the `program` attribute points to the folder that contains the test files you want to run.

### could not launch process: could not fork/exec

This usually happens in OSX due to signing issues. See the discussions in please see [#717](https://github.com/Microsoft/vscode-go/issues/717), [#269](https://github.com/Microsoft/vscode-go/issues/269) and [derekparker/delve/357](https://github.com/derekparker/delve/issues/357)

**_Solution_**: You may have to uninstall dlv and install it manually as per [instructions](https://github.com/derekparker/delve/blob/master/Documentation/installation/osx/install.md#manual-install)

### could not launch process: exec: "lldb-server": executable file not found in $PATH

This error can show up for Mac users using delve of version 0.12.2 or above. Not sure why, but doing a `xcode-select --install` has solved the problem for users who have seen this issue.