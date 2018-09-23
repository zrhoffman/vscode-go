This wiki page tracks the status of Go modules support in the Go extension for Visual Studio Code

https://github.com/golang/go/issues/24661 is the issue used by the Go tools team to track the update of Go modules support in various Go tools.

While that is in progress, the currently available [beta version](https://github.com/Microsoft/vscode-go/wiki/Use-the-beta-version-of-the-latest-Go-extension) of this extension has fixes for some of the features.

## Features that work in the beta version

- Go to definition, symbol info on hover and Signature Help when the setting `go.docsTool` is set to `gogetdoc` 
- `Go: Add Import` & `Go: Browse Packages` commands that will show the appropriate packages from the current module instead of GOPATH
- Auto-completion of unimported packages when the setting `go.autocompleteUnimportedPackages` is set to `true`


To ensure you have the latest Go tools with the Go modules support, please follow the below:
- Add the setting `"go.docsTool": "gogetdoc"` to use `gogetdoc` which drives the Go to definition feature
- Run the command `Go: Install/Update Tools`, choose `gogetdoc` and `gopkgs` from the list to update them

## Features not affected in the first place:
- Build : The build on save features as well as the `Go: Build ...` commands
- Test : Running tests via the `Go: Test` commands as well as the "run tests" codelens. 
- Generating of tests using the `Go: Generate ...` commands
- File Outline: Either via the Outline view in the explorer or using the command Cmd+Shift+O or Ctrl+Shift+O
- `Go: Add tags to struct fields` & `Go: Remove tags from struct fields` commands
- Code snippets
- Debugging

## Features that are broken, but we are in the process of fixing:
- Auto-completion
- Code coverage  

Please do try the [beta version](https://github.com/Microsoft/vscode-go/wiki/Use-the-beta-version-of-the-latest-Go-extension) and share any feedback/bugs you have.




