This page lists out all the settings that you can customize in the Go extension for Visual Studio Code

The following Visual Studio Code settings along with their *default* values that are available for the Go extension. If you want to change any of these, you can do so in user preferences (`cmd+,` or `ctrl+,`) or workspace settings (`.vscode/settings.json`). You don't have to copy these if you don't intend to change them.

```javascript
{
	"go.buildOnSave": true, 			// Run 'go build'/'go test -c' on save.
	"go.buildTags": "",					// The Go build tags to use for all commands that support a `-tags '...'` argument
	"go.buildFlags": [],				// Flags to `go build`/`go test` used during build-on-save or running tests. (e.g. ['-ldflags="-s"'])

	"go.lintOnSave": true,				// Run Lint tool on save.
	"go.lintTool": "golint",			// Specifies Lint tool name. Choices are `golint` and `gometalinter`
	"go.lintFlags": [],					// Flags to pass to Lint tool (e.g. ["-min_confidence=.8"])

	"go.vetOnSave": true,				// Run 'go tool vet' on save.
	"go.vetFlags": [],					// Flags to pass to `go tool vet` (e.g. ['-all', '-shadow'])

	"go.formatOnSave": true, 			// Runs formatting tool on save.
	"go.formatTool": "goreturns",		// Pick 'gofmt', 'goimports' or 'goreturns' to run on format.
	"go.formatFlags": [],				// Flags to pass to format tool (e.g. ['-s'])
	
	"go.testOnSave": false,				// Run 'go test' on save for current package. It is not advised to set this to `true` when you have Auto Save enabled.
	"go.coverOnSave": false,			// Run 'go test -coverprofile' on save
	"go.testTimeout": "30s",			// Specifies the timeout for go test in ParseDuration format.
	"go.testEnvVars": {},				// Environment variables that will passed to the process that runs the Go tests
	"go.testFlags": null,				// Flags to pass to `go test`. If null, then buildFlags will be used.
	
	"go.inferGopath": false,			// Infer GOPATH from the workspace root.
	"go.goroot": null,					// Specifies the GOROOT to use when no environment variable is set.
	"go.gopath": null,					// Specifies the GOPATH to use when no environment variable is set. The inferred GOPATH from workspace root overrides this, if go.inferGopath is set to true.
	"go.toolsGopath": "",				// Location to install the Go tools that the extension depends on if you don't want them in your GOPATH.

	"go.gocodeAutoBuild": false,					// Enable gocode's autobuild feature
	"go.useCodeSnippetsOnFunctionSuggest": false,	// Auto Complete functions with their parameter signature
	"go.autocompleteUnimportedPackages": false,		// Include unimported packages in auto-complete suggestions.

	"go.docsTool": "godoc",					// Pick 'godoc' or 'gogetdoc' to get documentation. In Go 1.5, godoc is used regardless of the choice here.
	"go.useLanguageServer": false			// Experimental: Not available in Windows. Use Go language server from Sourcegraph for Hover, Definition, Find All References, Signature Help, File Outline and Workspace Symbol features
	"go.addTags": {
		"tags": "json",					// Comma separated tags that will get added by the Add Tags command
		"options": "json=omitempty",	// Comma separated tag options that will get added by the Add Tags command. 
		"promptForTags": false			// If true, then user will be prompted to provide tags and options to be added by the Add Tags command.
	},
	"go.removeTags": {
		"tags": "",						// Comma separated tags that will get removed by the Remove Tags command. If empty, all tags are removed.
		"options": "",					// Comma separated tag options that will get removed by the Remove Tags command. 
		"promptForTags": false			// If true, then user will be prompted to provide tags and options to be removed by the Remove Tags command.
	},
	"go.editorContextMenuCommands": {	// Experimental Feature: Enable/Disable commands from the context menu in the editor.
		"toggleTestFile": true,
		"addTags": true,
		"testAtCursor": true,
		"generateTestForFunction": true,
		"addImport": false
		"removeTags": false,
		"testFile": false,
		"testPackage": false,
		"generateTestForFile": false,
		"generateTestForPackage": false,
		"testCoverage": false
	}
}
```