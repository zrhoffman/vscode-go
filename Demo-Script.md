## Machine setup

1. Install Go from https://golang.org/dl/.  
2. Choose a folder to use as your GOPATH workspace.  We'll use `$HOME/gopath`.
```bash
export GOPATH=$HOME/gopath
cd $GOPATH
```
3. Get all the Go tools that the extension depends on by running the command `Go: Install Tools`. Get sample code from below
```bash
# Sample code
go get -d github.com/Azure/azure-sdk-for-go/management
go get -u -v github.com/lukehoban/webapp-go
```
4. If on Mac OSX, follow the instructions at https://github.com/derekparker/delve/wiki/Building to install the Delve debugger.
4. Install Code `0.9.1` and launch it with Gallery support enabled:
```bash
code --enableExtensionGallery
```
5. Install the Go extension with `F1` then `Install Extension` then search for `Go`.
6. Turn on AutoSave under `File -> Auto Save`.
7. Relaunch Code on the `GOPATH` folder
```bash
code $GOPATH
```
8. Go to the debug viewlet, and click the gear icon.  Replace the generated launch.json with:
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

### IDE Features
| Demo        | Talking points  |
| ------------- |---------------|
| Show the installed extensions and highlight `Go`. | We used to have Go colorization, but with the new Go extension we are able to provide really rich Go language support inside Code. |
| Open `src/github.com/lukehoban/webapp-go/main.go`.  Navigate to the end of the file. | Colorization is based on a TextMAte bundle used by Atom and other text editors. |
| Hover over `viewHandler`.  Then hold down `cmd` while hovering.  Then left-click while holding down `cmd` and hovering. | We can get type information via QuickInfo, peek at the declaration of a function, and Go to Definition. |
| Hit `^-` to navigate back.  Hover over `listenAndServe` and do the same to navigate to definition. | We can use this to browse the implementation of the built-in Go libraries - including seeing their documentation. |
| Go-to-definition on `makeHandler`.  Create a new line after `fn(w, r, m[2])`. Type `validPath.FindStringSubmatch(r.URL)`. | We can get completion lists which helps us use the Go libraries correctly. |
| Hover over the red squiggle. Then fix by changing to `r.URL.Path`.  | We can also catch errors inside the editor. Here we used a URL instead of a String. |
| Optionally also show Find All References, Snippets, Outline and Formatting | There's a lot more IDE-like features available as well. |

### Debugging
| Demo        | Talking points  |
| ------------- |---------------|
| Delete the line that was just added.  Set a breakpoint on line `85`. | The really nice thing about Code is it's support for debugging - that's something that not many developer tools support yet for Go. |
| Hit `F5` to start debugging.  Wait for the breakpoint to be hit. | We set up our app to be debugged, so when we hit `F5` we'll hit our breakpoint. |
| In the callstack, navigate to each frame down the stack. | We can see the calling stack frames, down to the assembly code that launches the main goroutine. |
| Go back to `main.main` in the callstack, then set a breakpoint on line `34` and hit `F5` to continue. | Let's break on some more interesting code. |
| Open a browser and navigate to `localhost:8080/view/foo`.  Wait for the breakpoint to be hit. | We can see the locals at our breakpoint, including the `foo` article we just tried to load. |

 
