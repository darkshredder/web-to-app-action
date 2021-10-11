# web-to-app-action

Use this action to convert you website HTML/Web-assets to APK for Andriod.

## Inputs

### `build-folder-path`

**Optional**. Defaults to "build/", It is the path where HTML/web-assets are stored.

### `app-name`

**Optional**. Defaults to "MyApp", It is the name of your app whose APK is created.

### `output-folder-path`

**Optional**. Defaults to "apk/", It is the path where all types of APK are stored (Debug and Release).


## Example action workflow

```yaml
name: Convert build files to APK and upload to Github Artifacts
on: push

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16.x]

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
     
    - run: npm install
    - run: npm run build
 
    - uses: darkshredder/web-to-app-action@main
      with:
          build-folder-path: "build" # Defaults to build, It is the folder where build files or html are stored
          app-name: "Your-App-Name" # Defaults to MyApp
          output-folder-path: "my-apks" # Defaults to apk/, Where final APK files are created
    
    - name: 'Upload Artifact'
      uses: actions/upload-artifact@v2
      with:
        name: Final-apks
        path: my-apks/ # Should be same as "output-folder-path"
```
