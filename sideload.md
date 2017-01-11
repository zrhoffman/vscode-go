If you are working on the extension itself, you might want to sideload it to test it in Code. This case be done by preparing the extension and loading it directly.

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