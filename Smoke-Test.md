Pre-requisites for testing Go extension if you don't already have Go installed and the extension set up

1. Install [Go](https://golang.org/doc/install#install)
2. Setup GOPATH
       1. Choose a folder where you will be having the Go projects
       2. Add env variable GOPATH with value as the above folder path
       3. Create 3 folders "src", "bin" and "pkg"
3. Run `go get github.com/golang/example/hello`
4. Sideload the Go extension and open the folder $GOPATH/src/GitHub.com/golang/example in VS Code
5. Open any Go file. You will see "Analysis Tools Missing" in the status bar. Click on it to install the Go tools that the extension needs.


- Auto complete
- Auto complete for unimported packages 
- Signature Help 
- Snippets
- Hover Info 
- Goto and Peek Definition 
- Find References 
- File outline 
- Rename
- Build-on-save 
- Lint-on-save 
- Format 
- Generate unit tests squeleton
- Add Imports 
- Debugging 