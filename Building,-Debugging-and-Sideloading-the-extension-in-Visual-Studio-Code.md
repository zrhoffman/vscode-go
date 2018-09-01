You can set up a development environment for debugging the extension during extension development.

## Building and Debugging the extension

Ensure you have [node](https://nodejs.org/en/) installed.
Clone the repo, run `npm install` and open a development instance of Code.

```bash
git clone https://github.com/Microsoft/vscode-go
cd vscode-go
npm install
code .
```

You can now go to the Debug viewlet (`Ctrl+Shift+D`) and select `Launch Extension` then hit run (`F5`).

In the `[Extension Development Host]` instance that opens up, open any folder with Go code. Make sure the `window.openFoldersInNewWindow` setting is not `"on"`, otherwise a new, non-`[Extension Development Host]`, window may be opened.

You can now hit breakpoints and step through the extension.

If you make edits in the extension `.ts` files, just reload (`cmd-r`) the `[Extension Development Host]` instance of Code to load in the new extension code.  The debugging instance will automatically reattach.

To debug the debugger, see [the debugAdapter readme](/Microsoft/vscode-go/tree/master/src/debugAdapter).

## Running the tests
Tests may be run locally via the Debug viewlet: select `Launch Tests` then hit run (`F5`).

## Sideloading the extension
If you are working on the extension itself, you might want to sideload it to test it in Code. This can be done by preparing the extension and loading it directly.

1. make sure you have vsce installed globally: 

`npm install -g vsce`

2. git clone/pull this repo
3. cd into the repo
4. install the dependencies

`npm install`

5. build the package

`vsce package`

6. load the extension

Open the extensions menu in VSCode and choose `Install from VSIX` and select the `Go-xxx.vsix` file created by step 5.

## Beta testing this extension

If you want to help with testing the next update to this extension, its easy to do so. Please see [Beta testing the Go extension](https://github.com/Microsoft/vscode-go/wiki/Use-the-beta-version-of-the-latest-Go-extension)