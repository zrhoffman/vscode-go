## Machine setup

1. Install Go from https://golang.org/dl/.  
2. Choose a folder to use as your GOPATH workspace.  We'll use `$HOME/gopath`.
```bash
export GOPATH=$HOME/gopath
cd GOPATH
go get -d github.com/Azure/azure-sdk-for-go/management
```
3. Install Code `0.9.1` and launch it with Gallery support enabled:
```bash
code --enableExtensionGallery
```
4. Install the Go extension with `F1` then `Install Extension` then search for `Go`.
5. Relaunch Code on the `GOPATH` folder
```bash
code $GOPATH
```

## Demo script

