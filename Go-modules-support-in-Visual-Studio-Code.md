This wiki page tracks the status of Go modules support in the Go extension for Visual Studio Code

https://github.com/golang/go/issues/24661 is the issue used by the Go tools team to track the update of Go modules support in various Go tools.

While that is in progress, the latest version of this extension has fixes for some of the features.

## Features that work as of v0.6.90 

- Go to definition, symbol info on hover and Signature Help when the setting `go.docsTool` is set to `gogetdoc`. You will be prompted to update `gogetdoc`
- Go to definition feature if you havent changed the `go.docsTool` setting. You will be prompted to install a [fork](https://github.com/ianthehat/godef) of `godef` that we are testing.
- Auto-completion. You will be prompted to install a [fork](https://github.com/stamblerre/gocode) of `gocode` that we are testing as well as to update the `gopkgs` tool. Currently it only works if the package is already imported and used atleast once
- `Go: Add Import` & `Go: Browse Packages` commands that will show the appropriate packages from the current module instead of GOPATH


To ensure you have the latest Go tools with the Go modules support, and follow the prompts to install/update the required tools.

## Features not affected in the first place:
- Build : The build on save features as well as the `Go: Build ...` commands
- Test : Running tests via the `Go: Test` commands as well as the "run tests" codelens. 
- Generating of tests using the `Go: Generate ...` commands
- File Outline: Either via the Outline view in the explorer or using the command Cmd+Shift+O or Ctrl+Shift+O
- `Go: Add tags to struct fields` & `Go: Remove tags from struct fields` commands
- Code snippets
- Debugging


Please do try the [beta version](https://github.com/Microsoft/vscode-go/wiki/Use-the-beta-version-of-the-latest-Go-extension) and share any feedback/bugs you have.


