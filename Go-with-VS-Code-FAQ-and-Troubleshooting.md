## FAQ

**Q: I installed the plugin, but none of the features are working. Why?**

**A:** Make sure to install all the dependent Go tools. Run `Go: Install/Update Tools`. If you want to install only selected tools, then go through the [Go tools that this plugin depends on](https://github.com/Microsoft/vscode-go/wiki/Go-tools-that-the-Go-extension-depends-on) and install the ones you need manually

**Q: Why do my imported packages keep disappearing?**

**A:** By default, the plugin formats your code on save. To format, it uses the [goreturns](https://github.com/sqs/goreturns) tool that removes unused imports. You can add `"go.formatTool": "gofmt"` to your settings to use the gofmt tool instead which doesn't remove unused imports.

**Q: How do I just run my code? Not debug, just run.**

**A:** Use the keybinding `Ctrl+F5` or run the command `Debug: Start without Debugging` to run the file opened in the current editor.

**Q: Why is the GOPATH I set in the integrated terminal not being used by the plugin? Why isn't my program getting the environment variables I set in the integrated terminal?**

**A:** The extensions run in a separate process than the terminal or rest of the VS Code window. Therefore, environment variables set specifically in the integrated terminal is not visible to the extensions.

**Q: How does the plugin determine the GOPATH to use?**

**A:** See [GOPATH in the VS Code Go extension](https://github.com/Microsoft/vscode-go/wiki/GOPATH-in-the-VS-Code-Go-extension)

**Q: Auto-completions stopped working. What do I do?**

- Run `gocode close` in a terminal and try again.
- If it still doesnt work, run `go get -u github.com/nsf/gocode` to update the tool. If you use the `go.toolsGopath` setting, then set 
GOPATH to the value in that setting before running `go get` so that the tool is installed/updated in the right location
- If it still doesnt work, run `gocode -s -debug` in a terminal and try again. Results from `gocode` will show up in the terminal. 
If you see expected results in the terminal, but not in VS Code, log an issue in the [vscode-go](https://github.com/Microsoft/vscode-go) repo, else 
log an issue in the [gocode](https://github.com/nsf/gocode) repo.