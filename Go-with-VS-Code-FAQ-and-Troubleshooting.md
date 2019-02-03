## FAQ

**Q: I installed the plugin, but none of the features are working. Why?**

**A:** Make sure to install all the dependent Go tools. Run `Go: Install/Update Tools`. If you want to install only selected tools, then go through the [Go tools that this plugin depends on](https://github.com/Microsoft/vscode-go/wiki/Go-tools-that-the-Go-extension-depends-on) and install the ones you need manually

**Q: I see "git pull --ff-only" errors when installing tools.**

**A:** Chances are that there was a force pushed commit to the repo for the tool being installed. Delete the folder corresponding to this tool in your `$GOPATH/src` (if you have set `go.toolsGopath`, then check there) and try again.

**Q: Why do my imported packages keep disappearing?**

**A:** By default, the plugin formats your code on save. To format, it uses the [goreturns](https://github.com/sqs/goreturns) tool that removes unused imports. You can add `"go.formatTool": "gofmt"` to your settings to use the gofmt tool instead which doesn't remove unused imports.

**Q: How does the plugin determine the GOPATH to use?**

**A:** See [GOPATH in the VS Code Go extension](https://github.com/Microsoft/vscode-go/wiki/GOPATH-in-the-VS-Code-Go-extension)

**Q: Does VS Code support Go modules?**

**A:** See [Go modules support in VS Code](https://github.com/Microsoft/vscode-go/wiki/Go-modules-support-in-Visual-Studio-Code)

**Q: Can I use language server when using Go modules?**

**A:** Currently, there are 3 language servers in the market for Go. The one from go-langserver from Sourcegraph, bingo by @saibing and go-lsp from Google

- The Go language server by Sourcegraph does not support modules and has stopped adding new features
- If you want to use bingo as your language server, then see https://github.com/Microsoft/vscode-go/wiki/Go-modules-support-in-Visual-Studio-Code#updates-as-of-080
- The language server from Google is work in progress.


**Q: How do I just run my code? Not debug, just run.**

**A:** Use the keybinding `Ctrl+F5` or run the command `Debug: Start without Debugging`.

Behind the scenes, we use `go run` command which takes a file path. Therefore, If you already have a `launch.json` file with default configuration, update it to use `${file}` instead of `${fileDirname}` instead. If you are using your own debug configuration, ensure that the `program` property needs to point to a file and not directory.

In the absence of a file path in the `program` property, `Start without Debugging` falls back to normal debugging

**Q: Why is the GOPATH I set in the integrated terminal not being used by the plugin? Why isn't my program getting the environment variables I set in the integrated terminal?**

**A:** The extensions run in a separate process than the terminal or rest of the VS Code window. Therefore, environment variables set specifically in the integrated terminal is not visible to the extensions.

**Q: Auto-completions stopped working. What do I do?**

- If this is for symbols from external packages, then ensure they installed first. You can do this by either running `Go: Build Current Package` which will install all dependencies or install the dependencies manually yourself using `go install`.
- If it still doesnt work, run `gocode close` or `gocode exit` in a terminal and try again. Use `gocode-gomod` instead of `gocode` if you are using Go modules.
- If it still doesnt work, run `Go: Install/Update Tools`, choose `gocode` to update the tool. Choose `gocode-gomod` if you are using Go modules
- If it still doesnt work, run `gocode close` or `gocode exit` followed by `gocode -s -debug` in a terminal and try again. Results from `gocode` will show up in the terminal. Use `gocode-gomod` instead of `gocode` if you are using Go modules.
If you see expected results in the terminal, but not in VS Code, log an issue in the [vscode-go](https://github.com/Microsoft/vscode-go) repo, else 
log an issue in the [gocode](https://github.com/mdempsky/gocode) repo. If you are using Go modules, log the issue in https://github.com/stamblerre/gocode

**Q: Why doesn't formatting doesn't work on file save?**

**A:** Check the console (Help -> Toggle Developer Tools -> Console) for messages like "Formatting took too long" or "Format On Save feature could be aborted". If you find such a message, then chances are formatted was aborted because it took too long and so can affect the save experience. You can control this timeout using the setting `editor.formatOnSaveTimeout`

**Q: My imports have red lines saying "package not found"**

**A:** These are build errors. Go to View -> Output -> Select "Go" from the dropdown on the top right corner of the panel. Here you can see the output of the `go build` (or `go test` if the current file is a test file). Copy the `go build` command along with arguments and try running it in the terminal. If you still see the same errors, then the problem is in your setup of GOPATH. If it runs fine, then log an issue and we can look into it

**Q: How do I get the features/bug fixes that are implemented but not released yet? How do I get the beta version of the Go extension?**

**A:** See [Install the beta version](https://github.com/Microsoft/vscode-go/wiki/Use-the-beta-version-of-the-latest-Go-extension)