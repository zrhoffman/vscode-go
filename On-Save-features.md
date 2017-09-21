The Go extension runs the below on each file save by default. You can turn them off in [settings](https://github.com/Microsoft/vscode-go/wiki/On-Save-features).
* Build
* Lint
* Vet
* Format

The below can be enabled to run on file save by turning them on in settings
* Test
* Code Coverage

## Build on save
Since `go build` ignores test files, we use `go test -i -c -o` instead on the current package. This will compile the whole package. 

You can set `go.buildOnSave` to `workspace` to run the same for all the packages in the workspace. 

## Lint on save

A linter is a tool giving coding style feedback and suggestions.
By default this extension uses the official [golint](https://github.com/golang/lint) as a linter.

You can change the default linter and use the more advanced [Go Meta Linter](https://github.com/alecthomas/gometalinter)
by setting `go.lintTool` to "gometalinter" in your settings.

Go meta linter uses a collection of various linters which will be installed for you by the extension.

Some of the very useful linter tools:
* [errcheck](https://github.com/kisielk/errcheck) checks for unchecked errors in your code.
* [varcheck](https://github.com/opennota/check) finds unused global variables and constants.
* [deadcode](https://github.com/tsenart/deadcode) finds unused code.

If you want to run only specific linters (some linters are slow), you can modify your configuration to specify them:

```javascript
  "go.lintFlags": ["--disable-all", "--enable=errcheck"],
```

Alternatively, you can use [megacheck](https://github.com/dominikh/go-tools/tree/master/cmd/megacheck) which 
may have significantly better performance than `gometalinter`, while only supporting a subset of the tools.

To disable lint on save turn off `go.lintOnSave`

## Format on save

If you have Auto Save feature enabled, then you might want to disable the format on save feature so that the code doesnt keep changing under you. You can do this by disabling the `go.formatOnSave` setting.

By default, `goreturns` is the tool used for formatting. You can choose `goimports` or `gofmt` by changing the `go.formatTool` setting

If you see your unused imports disappearing or unimported packages getting added automatically, thats the `goreturns` tool doing the magic behind the scenes.




