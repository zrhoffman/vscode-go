This wiki page captures changes/features/bug fixes for each release of the Go extension from version 0.6.40


## Upcoming release
* New configuration `go.formatFlags` to pass flags to the formatting tool
* New configuration `go.testEnVars` to pass environment variables to Go tests
* New command to execute the last run test. The command is `Go: Test Previous`
* Enable Undo after Rename. Fix for [#13](https://github.com/Microsoft/vscode-go/issues/13)
* New commands to generate unit test skeletons using `gotests` tool. Needs Go 1.6 or higher. The commands are
   * Go: Generate unit tests for current file
   * Go: Generate unit tests for current function
   * Go: Generate unit tests for current package
* Enable autocomplete for functions from unimported packages and for unimported packages themselves. See the feature requests [#407](https://github.com/Microsoft/vscode-go/issues/407) or [#437](https://github.com/Microsoft/vscode-go/issues/437) for details
* Send test output to a distinct output channel
* Changes made to GOROOT and GOPATH via settings now take effect immediately without requiring to reload/restart VS Code
* Go extension ready to use after installing tools without requiring to reload/restart VS Code


## 0.6.43 - August 2016
* New command to install/update all the Go tools that the Go extension is dependent on. The command is `Go: Install Tools`
* Auto-generated launch.json to have `showLog:true`. For more details see #412
* Updates to Extra Info feature: Documentation from `godoc` now appears on hover 

## 0.6.40-42 - July 2016
* Option to choose `gometalinter` as tool for linting
* New configuration `showLog` to toggle the debugging output from `delve`
* Better logging while installing tools