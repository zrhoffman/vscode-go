You can set up a development environment for debugging the extension during extension development.

## Building and Debugging the extension

Clone the repo, run `npm install` and open a development instance of Code.

```bash
git clone https://github.com/Microsoft/vscode-go
cd vscode-go
npm install
code .
```

You can now go to the Debug viewlet and select `Launch Extension` then hit run (`F5`).

In the `[Extension Development Host]` instance, open any folder with Go code.

You can now hit breakpoints and step through the extension.

If you make edits in the extension `.ts` files, just reload (`cmd-r`) the `[Extension Development Host]` instance of Code to load in the new extension code.  The debugging instance will automatically reattach.

To debug the debugger, see [the debugAdapter readme](/Microsoft/vscode-go/tree/master/src/debugAdapter).

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