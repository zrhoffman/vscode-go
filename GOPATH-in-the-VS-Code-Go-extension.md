Out of the box, the extension uses the value of the environment variable `GOPATH`. From Go 1.8 onwards, if no such environment variable is set, then the default GOPATH as deciphered from the command `go env` is used.

Setting `go.gopath` in User settings overrides the GOPATH that was derived from the above logic.
Setting `go.gopath` in Workspace settings overrides the one from User settings.
You can set multiple folders as GOPATH in this setting. Note that they should be `;` separated in Windows and `:` separated otherwise.

Setting `go.inferGopath` overrides all of the above. If `go.inferGopath` is set to true, the extension will try to infer the `GOPATH` from the path of the workspace i.e. the directory opened in `vscode`. It searches upwards in the path for the `src` directory, and sets `GOPATH` to one level above that.

For example, if your project looks like `/aaa/bbb/ccc/src/...`, then opening the directory `/aaa/bbb/ccc/src` (or anything below that) will cause the extension to search upwards, find the `src` component in the path, and set the `GOPATH` to one level above that i.e. `GOPATH=/aaa/bbb/ccc`. 

This setting is useful when you are working on different Go projects which have different GOPATHs. Instead of setting the GOPATH in the workspace settings of each project, you can just set `go.inferGopath` to `true`and the extension uses the right GOPATH automatically.

By default, all the dependent Go tools are used from the GOPATH derived from the above logic. If they are available on your PATH, the PATH is used to locate the Go tools. If the Go tools are not in your path, you might end up with the same Go tools installed in each of your GOPATHs. To prevent the Go tools from cluttering your GOPATH, use the `go.toolsGopath` setting to provide a location for the Go tools. 