name: Build Android APK

on:
  push:
    branches: [ "main" ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Set up JDK 17
      uses: actions/setup-java@v4
      with:
        java-version: '17'
        distribution: 'temurin'

    - name: Extract Zip and Build APK
      run: |
        sudo apt-get install -y unzip
        
        for file in *.zip; do
          if [ -f "$file" ]; then
            echo "Unzipping $file..."
            unzip -o "$file"
          fi
        done

        GRADLEW_PATH=$(find . -name "gradlew" -type f | head -n 1)

        if [ -z "$GRADLEW_PATH" ]; then
          echo "Error: gradlew file not found!"
          exit 1
        fi

        PROJECT_DIR=$(dirname "$GRADLEW_PATH")
        cd "$PROJECT_DIR"
        chmod +x gradlew
        ./gradlew assembleDebug

    - name: Upload APK Artifact
      uses: actions/upload-artifact@v4
      with:
        name: app-debug
        path: '**/build/outputs/apk/debug/*.apk'
        
