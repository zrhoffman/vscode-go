## Machine setup

1. Install Go from https://golang.org/dl/.  
2. Choose a folder to use as your GOPATH workspace.  We'll use `$HOME/gopath`.
```bash
export GOPATH=$HOME/gopath
cd GOPATH
```
3. Get tools and samples (Note - the extension should offer to auto-install these tools - but for fewer moving pieces we'll just install them in advance):
```bash
# Go tools
go get -u -v github.com/derekparker/delve/cmd/dlv
go get -u -v golang.org/x/tools/cmd/gorename
go get -u -v github.com/nsf/gocode
go get -u -v sourcegraph.com/sqs/goreturns
go get -u -v github.com/rogpeppe/godef
go get -u -v github.com/golang/lint/golint
go get -u -v github.com/lukehoban/go-find-references
# Sample code
go get -d github.com/Azure/azure-sdk-for-go/management

```
4. Install Code `0.9.1` and launch it with Gallery support enabled:
```bash
code --enableExtensionGallery
```
5. Install the Go extension with `F1` then `Install Extension` then search for `Go`.
6. Relaunch Code on the `GOPATH` folder
```bash
code $GOPATH
```
7. Go to the debug viewlet, and click the gear icon.  Replace the generated launch.json with:
```json
{
    "version": "0.1.0",
    "configurations": [{
        "name": "webapp-go",
        "type": "go",
        "program": "src/github.com/lukehoban/webapp-go/main.go"
    }]
}
```

## Demo script


| Demo        | Talking points  |
| ------------- |---------------|
| Show the installed extensions and highlight `Go`. | We used to have Go colorization, but with the new Go extension we are able to provide really rich Go language support inside Code. |
| Open `src/github.com/lukehoban/webapp-go/main.go`.  Navigate to the end of the file. | Colorization is based on a TextMAte bundle used by Atom and other text editors. |
| Hover over `viewHandler`.  Then hold down `cmd` while hovering.  Then left-click while holding down `cmd` and hovering. | We can get type information via QuickInfo, peek at the declaration of a function, and Go to Definition. |

 
