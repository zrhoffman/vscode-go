The Go extension for Visual Studio Code various Go tools, installed in the user's GOPATH. Some of them are responsible for general language features like code navigation, auto-completions, symbol search etc. Others, while helpful are optional for the Go extension to provide day-to-day language support.

Tools essential for the general features of this extension:

- [gocode](https](//github.com/nsf/gocode) for auto-completion
- [go-outline](https://github.com/ramya-rao-a/go-outline) for symbol search in the current file
- [go-symbols](https://github.com/acroca/go-symbols) for symbol search in the current workspace
- [gopkgs](https://github.com/uudashr/gopkgs/cmd/gopkgs) for auto-completion of unimported packages
- [guru](https://golang.org/x/tools/cmd/guru) for the `Find all References` feature
- [gorename](https://golang.org/x/tools/cmd/gorename) for renaming symbols
- [goreturns](https://sourcegraph.com/sqs/goreturns)or [goimports](https://golang.org/x/tools/cmd/goimports) for formatting code
- [godef](https://github.com/rogpeppe/godef) or [gogetdoc](https://github.com/zmb3/gogetdoc) for the `Go to Definition` feature
- [godoc](https://golang.org/x/tools/cmd/godoc) or [gogetdoc](https://github.com/zmb3/gogetdoc) for the documentation that appears on hover
- [golint](https://github.com/golang/lint/golint) or [gometalinter](https://github.com/alecthomas/gometalinter) or  [megacheck](https://honnef.co/go/tools/) for linting
- [dlv](https://github.com/derekparker/delve/cmd/dlv) for debugging

If any of these tools are missing, you will see an "Analysis Tools Missing" warning in the bottom right corner of the editor.  Clicking it will offer to install the missing tools for you.

There are other features of this extension which you most probably wouldn't be using every day. For eg: Generating unit tests or generating stubs for interface or modify tags. The tools used for such features are:

- [gomodifytags](https:///fatih/gomodifytags) for modifying tags on structs
- [goplay](https:///haya14busa/goplay/cmd/goplay) for running current file in the Go playground
- [impl](https:///josharian/impl) for generating stubs for interfaces
- [gotype-live](https:///tylerb/gotype-live) for providing diagnostics as you type
- [gotests](https://github.com/cweill/gotests/) for generating unit tests
- [go-langserver](https://github.com/sourcegraph/go-langserver) for using the Go language server by Sourcegraph

You can install all these tools at once by running the command `Go: Install/Update Tools`. The same command can be used to keep the tools up to date as well as to re-compile in case you change the version of Go being used.

If you wish to have the extension use a separate GOPATH for its tools, provide the desired location in the setting `go.toolsGopath`.

To install the tools manually in the current GOPATH, just copy the below (after choosing the tools) in your terminal run:

```bash
go get -u -v github.com/ramya-rao-a/go-outline
go get -u -v github.com/acroca/go-symbols
go get -u -v github.com/nsf/gocode
go get -u -v github.com/rogpeppe/godef
go get -u -v golang.org/x/tools/cmd/godoc
go get -u -v github.com/zmb3/gogetdoc
go get -u -v github.com/golang/lint/golint
go get -u -v github.com/fatih/gomodifytags
go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs
go get -u -v golang.org/x/tools/cmd/gorename
go get -u -v sourcegraph.com/sqs/goreturns
go get -u -v golang.org/x/tools/cmd/goimports
go get -u -v github.com/cweill/gotests/...
go get -u -v golang.org/x/tools/cmd/guru
go get -u -v github.com/josharian/impl
go get -u -v github.com/haya14busa/goplay/cmd/goplay
go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs
go get -u -v github.com/fatih/gomodifytags
```

And for debugging:

- delve: Follow the instructions at https://github.com/derekparker/delve/blob/master/Documentation/installation/README.md.