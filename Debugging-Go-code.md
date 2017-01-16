# Install delve

To use the debugger, you must currently manually install `delve`.  See the [Installation Instructions](https://github.com/derekparker/delve/tree/master/Documentation/installation) for full details.  On OS X it requires creating a self-signed cert to sign the `dlv` binary.

Based on how you install delve it will either end up in your PATH or GOPATH. 
If it ends up in your GOPATH which you have only set in user/workspace settings, then the Go extension cannot find it. Therefore, either ensure that `dlv` is in your path or ensure that GOPATH is set outside of VS Code so that the Go extension can find it.

# Set up configurations in launch.json

Once delve is installed, you can either press `F5` or go to the Code debug viewlet and select the configuration gear. Select `Go` if there is a popup asking you to select your environment. This will create a `launch.json` file which will contain the configurations for debugging. By default, there would be a single configuration as below:

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

The `program` option can refer to a package folder to debug, or a file within that folder.

The `mode` parameter can be set to:

* `debug` to compile the contents of the program folder and launch under the debugger. [default]
* `test` to debug tests in the program folder. To debug a single test, pass `-test.run` and the Test name as args.
* `exec` to run a pre-built binary specified in program, for example `"program":"${workspaceRoot}/mybin"`.
* `remote` to attach to a remote headless Delve server.  You must manually run Delve on the remote machine, and provide the additional `remotePath`, `host` and `port` debug configuration options pointing at the remote machine.

The debugger cannot read GOPATH from the user/workspace settings. Therefore, if you want to use a GOPATH that is different from the one set outside of VS Code, then set it in the `env` property in the launch.json file.

# Remote Debugging

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

# Troubleshooting

## `Cannot find Delve debugger at ... Ensure it is in your "GOPATH/bin" or "PATH".

Like the error message says, the extension cannot find `dlv`. 
This can happen if `dlv` got installed to your GOPATH which you have set using `go.gopath` in the settings.
Since the debug adapter cannot read the settings, it is not aware of this GOPATH.

_Solution_: You can either set the GOPATH as an env var or point PATH to the dlv binary.

## `Cannot find package ".." in any of ... 

If you have set GOPATH using `go.gopath` in your settings, then the debug adapter cannot read it as the it is not aware of the settings. 

_Solution_: Add the GOPATH as an env var in the `env` property in the `launch.json` file.

