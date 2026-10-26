name: Build KeyCheck Dylib

on: [push]

jobs:
  build:
    runs-on: macos-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Compile .mm to .dylib
      run: |
        echo "Bắt đầu biên dịch file tweak.mm..."
        clang++ -dynamiclib -o mytweak.dylib tweak.mm -framework Foundation -framework UIKit -stdlib=libc++
        echo "Biên dịch thành công!"

    - name: Upload Artifact
      uses: actions/upload-artifact@v4
      with:
        name: keycheck-dylib
        path: mytweak.dylib
