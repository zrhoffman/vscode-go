The following are Visual Studio Code settings along with their *default* values that are available for the Go extension. If you want to change any of these, you can do so in user preferences (`cmd+,` or `ctrl+,`) or workspace settings (`.vscode/settings.json`). You don't have to copy these if you don't intend to change them.


Setting | Default Value | Description
------- | ------------- | -----------
go.buildOnSave | `true` | Run `go build` on save. If on test file, then `go test -c` is run on save
go.buildTags | `""` | The Go build tags to use for all commands that support a `-tags '...'` argument
go.buildFlags | `[]` | Flags to `go build`/`go test` used during build-on-save or running tests. (e.g. ['-ldflags="-s"'])
go.lintOnSave | `true` | Run Lint tool on save.
go.lintTool | "golint" | Specifies Lint tool name. Choices are `golint` and `gometalinter`
go.lintFlags | `[]` | Flags to pass to Lint tool (e.g. ["-min_confidence=.8"])
go.vetOnSave | `true` | Run 'go tool vet' on save.
go.vetFlags | `[]` | Flags to pass to `go tool vet` (e.g. ['-all', '-shadow'])
go.formatOnSave | `true` | Run formatting tool on save.
go.formatTool | "goreturns" | Specifies formatting tool to use. Choices are 'gofmt', 'goimports' or 'goreturns'
go.formatFlags | `[]` | Flags to pass to format tool (e.g. ['-s'])
go.testOnSave | `false` | Run 'go test' on save for current package. It is not advised to set this to `true` when you have Auto Save enabled.
go.coverOnSave | `false` | Run 'go test -coverprofile' on save
go.coverageOptions |  | Choose between "showCoveredCodeOnly", "showUncoveredCodeOnly" and "showBothCoveredAndUncoveredCode". Default is "showBothCoveredAndUncoveredCode". Use these options to control whether only covered or only uncovered code or both should be highlighted after running test coverage
go.testTimeout | "30s" | Specifies the timeout for go test in ParseDuration format.
go.testEnvVars |  {} |  Environment variables that will passed to the process that runs the Go tests
go.testFlags |  null |  Flags to pass to `go test`. If null, then buildFlags will be used.
go.inferGopath |  `false` | Infer GOPATH from the workspace root.
go.goroot |  null |  Specifies the GOROOT to use when no environment variable is set.
go.gopath |  null |  Specifies the GOPATH to use when no environment variable is set. The inferred GOPATH from workspace root overrides this, if go.inferGopath is set to true.
go.toolsGopath |  "" | Location to install the Go tools that the extension depends on if you don't want them in your GOPATH
go.toolsEnvVars | `{}` | Environment variables that will passed to the processes that run the Go tools (e.g. CGO_CFLAGS)
go.gocodeAutoBuild |  `false` |  Enable gocode's autobuild feature
go.useCodeSnippetsOnFunctionSuggest |  `false` | Auto Complete functions with their parameter signature
go.autocompleteUnimportedPackages |  `false` | Include unimported packages in auto-complete suggestions
go.docsTool |  "godoc" |  Pick 'godoc' or 'gogetdoc' to get documentation. In Go 1.5, godoc is used regardless of the choice here.
go.useLanguageServer |  `false` | Experimental: Not available in Windows. Use Go language server from Sourcegraph for Hover, Definition, Find All References, Signature Help, File Outline and Workspace Symbol features
go.addTags | | Comma separated tags and options used by the `Go: Add Tags` command. Set `promptForTags` to `true` to be prompted for tags when the `Go: Add Tags` command is run. See https://github.com/fatih/gomodifytags to learn more about how these settings are used. Default value is: `{ "tags": "json", "options": "json=omitempty", "promptForTags": false }`
go.removeTags | | Comma separated tags and options used by the `Go: RemoveTags` command. Set `promptForTags` to `true` to be prompted for tags when the `Go: RemoveTags` command is run. See https://github.com/fatih/gomodifytags to learn more about how these settings are used. Default value is : `{ "tags": "", "options": "", "promptForTags": false }`
go.editortorContextMenuCommands | | Experimental Feature: Enable/Disable commands from the context menu in the editor. Default value is: `{ "toggleTestFile": true, "addTags": true, "testAtCursor": true, "generateTestForFunction": true, "addImport": false, "removeTags": false, "testFile": false, "testPackage": false, "generateTestForFile": false, "generateTestForPackage": false, "testCoverage": false }`
go.liveErrors | `{"enabled": true, "delay": 500 }` | Use gotype on the file currently being edited and report any semantic or syntactic errors found after configured delay post keystroke
go.referencesCodeLens.enabled | `true` | Shows reference count above functions using codelens.

