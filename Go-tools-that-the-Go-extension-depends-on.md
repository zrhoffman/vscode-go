The Go extension for Visual Studio Code uses the following tools, installed in the user's GOPATH.  If any tools are missing, you will see an "Analysis Tools Missing" warning in the bottom right corner of the editor.  Clicking it will offer to install the missing tools for you.

You can install all these tools at once by running the command `Go: Install/Update Tools`. The same command can be used to keep the tools up to date as well as to re-compile in case you change the version of Go being used.

If you wish to have the extension use a separate GOPATH for its tools, provide the desired location in the setting `go.toolsGopath`.

- go-outline: `go get -u -v github.com/ramya-rao-a/go-outline`
- go-symbols: `go get -u -v github.com/acroca/go-symbols`
- gocode: `go get -u -v github.com/nsf/gocode`
- godef: `go get -u -v github.com/rogpeppe/godef`
- godoc: `go get -u -v golang.org/x/tools/cmd/godoc`
- gogetdoc: `go get -u -v github.com/zmb3/gogetdoc`
- golint: `go get -u -v github.com/golang/lint/golint`
- gomodifytags: `go get -u -v github.com/fatih/gomodifytags`
- gopkgs: `go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs`
- gorename: `go get -u -v golang.org/x/tools/cmd/gorename`
- goreturns: `go get -u -v sourcegraph.com/sqs/goreturns`
- gotests: `go get -u -v github.com/cweill/gotests/...`
- guru: `go get -u -v golang.org/x/tools/cmd/guru`
- impl: `go get -u -v github.com/josharian/impl`

To install the tools manually in the current GOPATH, just paste and run:
```bash
go get -u -v \
    github.com/ramya-rao-a/go-outline \
    github.com/acroca/go-symbols \
    github.com/nsf/gocode \
    github.com/rogpeppe/godef \
    golang.org/x/tools/cmd/godoc \
    github.com/zmb3/gogetdoc \
    github.com/golang/lint/golint \
    github.com/fatih/gomodifytags \
    github.com/uudashr/gopkgs/cmd/gopkgs \
    golang.org/x/tools/cmd/gorename \
    sourcegraph.com/sqs/goreturns \
    github.com/cweill/gotests/... \
    golang.org/x/tools/cmd/guru \
    github.com/josharian/impl
```

And for debugging:

- delve: Follow the instructions at https://github.com/derekparker/delve/blob/master/Documentation/installation/README.md.