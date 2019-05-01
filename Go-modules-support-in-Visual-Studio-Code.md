_This wiki page tracks the status of Go modules support in the Go extension for Visual Studio Code_

To get Go module support in VS Code, ensure that you have the latest Go extension and use the new language server [gopls](https://github.com/golang/go/wiki/gopls) from Google by adding the below in your settings
```json
// The only setting you need in version 0.10.0 and above to use gopls
"go.useLanguageServer": true
```

If you are on version lower than 0.10.0 of this extension, then you will need to install [gopls](https://github.com/golang/go/wiki/gopls) manually and add the below extra setting to use the language server from Google
```json
  // All the settings you need in version lower than 0.10.0 in order to tell this extension
  // to use `gopls` instead of `go-langserver` as the language server
  "go.useLanguageServer": true
  "go.alternateTools": {
    "go-langserver": "gopls", 
  },
  "go.languageServerExperimentalFeatures": {
    "format": true,
    "autoComplete": true
  }
```

Remember to update your version of `gopls` from time to time using `Go: Install/Update Tools` so that you keep getting the improvements that are being made to the language server.

If you don't want to use the language server for any reason, then please know that not all the [Go tools](https://github.com/Microsoft/vscode-go/wiki/Go-tools-that-the-Go-extension-depends-on) that this extension depends on supports Go modules. https://github.com/golang/go/issues/24661 is the issue used by the Go tools team to track the update of Go modules support in various Go tools.

## FAQ

### Can I use the language server when using Go modules?

Yes, you can! Please see the section right above this question for details

### Why is code navigation and code completion slow when using Go modules?

This is mostly due to the limitation of the tools that power these features which are `godef` and `gocode` respectively. The Go tools team at Google are working on improving them and also working on a [language server](https://godoc.org/golang.org/x/tools/cmd/gopls) which will be the long term solution for all language features.

Please try out the language server as described in the first section of this page.
If you don't want to use the language server then,
- For slowness in code completion, log an issue in the [gocode repo](https://github.com/stamblerre/gocode).
- For slowness in code navigation, log an issue in the [godef repo](https://github.com/rogpeppe/godef) or if you chosen to `gogetdoc` in your settings, then log an issue in the [gogetdoc repo](https://github.com/zmb3/gogetdoc)

Code navigation and code completion definitely works better when using the language server from Google. So, please give that a try. Check the previous question on this wiki to learn how to enable the language server.

### Auto import no longer happens on file save. Why?

If you are using the language server `gopls`, and are on version lower than `0.10.2` of this extension, then please add the below to your settings to get missing imports added when you save your file
```
"[go]": {
    "editor.codeActionsOnSave": {
        "source.organizeImports": true
    },
}
```

If you are not using the language server, 
- This extension uses [goreturns](https://github.com/sqs/goreturns) tool by default to format your files and auto import missing packages. Since this tool doesn't support modules, the auto import feature on file save no longer works.
- Add the setting `"go.formatTool": "goimports"` and then use `Go: Install/Update Tools` to install/update `goimports` as it has recently added support for modules.

## Updates as of 0.10.2
The below settings are set by default, so you don't need to add them specifically to get the adding of missing imports and removal of unused imports feature when you save your file while using `gopls`
```
"[go]": {
    "editor.codeActionsOnSave": {
        "source.organizeImports": true
    },
}
```


## Updates as of 0.10.0

We now officially support `gopls`, the language server from Google. Please follow the instructions at the top of this page to use it.

## Updates as of 0.9.0

- Module support is now available in the main repo for `godef` and so we no longer rely on its fork. As a result, you will no longer need `godef-gomod`. You will be prompted to update your version of `godef` though.
- Go to definition with sub modules will now work when the main module is opened in VS Code. Note: The second jump from sub-modules still won't work and this is being tracked in https://github.com/Microsoft/vscode-go/issues/2296
- `goimports` now supports formatting with modules. Change your `go.formatTool` setting to `goimports` and use `Go: Install/Update Tools` to update it to ensure you have the latest changes.


## Features that work as of v0.6.91 

Apart from what we have already achieved in v0.6.90, the below are available in the current [beta version](https://github.com/Microsoft/vscode-go/wiki/Use-the-beta-version-of-the-latest-Go-extension)

- **Code Coverage**
- **Clickable links in the test output** to files where tests are failing.

## Features that work as of v0.6.90 

- **Go to definition, symbol info on hover and Signature Help** 
    - These features will work as expected when the setting `go.docsTool` is set to `gogetdoc`. 
    - You will be prompted to update `gogetdoc`
- **Go to definition** feature 
    - If you havent changed the `go.docsTool` setting, you will be prompted to install a [fork](https://github.com/ianthehat/godef) of `godef` that we are testing. 
    - _Note_: This feature may be slower than usual because the fork depends on `go list` which itself is slower when using modules.
- **Auto-completion**. 
    - You will be prompted to install a [fork](https://github.com/stamblerre/gocode) of `gocode` that we are testing as well as to update the `gopkgs` tool. 
    - Currently it only works if the package is already imported and used atleast once. 
    - _Note_: This feature may be slower than usual because the fork depends on `go list` which itself is slower when using modules.
- **`Go: Add Import` & `Go: Browse Packages`** commands 
    - These commands will show the appropriate packages from the current module instead of GOPATH
- **Formatting**
    - `goimports` and `goreturns` do not support Go modules yet. So, to get the formatting feature, add `"go.formatTool": "gofmt"` in your settings.

To ensure you have the latest Go tools with the Go modules support, and follow the prompts to install/update the required tools.

## Features not affected in the first place:
- **Build** : The build on save features as well as the `Go: Build ...` commands
- **Test** : Running tests via the `Go: Test` commands as well as the "run tests" codelens. 
- **Generating of tests** using the `Go: Generate ...` commands
- **File Outline**: Either via the Outline view in the explorer or using the command Cmd+Shift+O or Ctrl+Shift+O
- **Modify tags on struct fields**: `Go: Add tags to struct fields` & `Go: Remove tags from struct fields` commands
- **Code snippets**
- **Debugging**

## Features that arent working yet

These are tracked as issues and have the label [go-modules](https://github.com/Microsoft/vscode-go/issues?q=is%3Aopen+is%3Aissue+label%3Ago-modules)