# Deploy to GitHub Pages

This repository is configured to automatically build and deploy Space Cadet Pinball to GitHub Pages.

## Prerequisites

**Important**: You need the original game resource files (not included due to copyright). Place all game files (excluding the .exe) in the `game_resources/` directory before building.

## Automatic Deployment (Recommended)

1. **Enable GitHub Pages** in your repository:
   - Go to **Settings** → **Pages**
   - Under "Build and deployment":
     - Source: **GitHub Actions**
   - Save

2. **Add game resources**:
   - Place original game files in `game_resources/` folder
   - Commit and push to your repository

3. **Push changes**:
   ```bash
   git add .
   git commit -m "Deploy to GitHub Pages"
   git push
   ```

4. The GitHub Action will automatically:
   - Install Emscripten
   - Build the project for WebAssembly
   - Deploy to GitHub Pages

5. **Access your game** at: `https://<your-username>.github.io/<repository-name>/`

## Manual Local Build

If you want to build locally:

### Windows (PowerShell)

1. **Install Emscripten**:
   ```powershell
   git clone https://github.com/emscripten-core/emsdk.git
   cd emsdk
   .\emsdk.bat install latest
   .\emsdk.bat activate latest
   .\emsdk_env.ps1
   ```

2. **Install CMake and Ninja** (if not already installed):
   ```powershell
   winget install Kitware.CMake
   winget install Ninja-build.Ninja
   ```

3. **Build the project**:
   ```powershell
   cd path\to\SpaceCadetPinball-master
   mkdir build-web
   cd build-web
   emcmake cmake -G Ninja ..
   cmake --build .
   ```

4. **Output files** will be in the `bin/` directory:
   - `SpaceCadetPinball.html` (rename to `index.html` for GitHub Pages)
   - `SpaceCadetPinball.js`
   - `SpaceCadetPinball.wasm`
   - `SpaceCadetPinball.data`

### Linux

1. **Install dependencies**:
   ```bash
   # Install Emscripten
   git clone https://github.com/emscripten-core/emsdk.git
   cd emsdk
   ./emsdk install latest
   ./emsdk activate latest
   source ./emsdk_env.sh
   
   # Install build tools
   sudo apt-get update
   sudo apt-get install -y cmake ninja-build
   ```

2. **Build**:
   ```bash
   cd path/to/SpaceCadetPinball-master
   mkdir build-web
   cd build-web
   emcmake cmake -G Ninja ..
   cmake --build .
   ```

## Troubleshooting

- **Game resources not found**: Make sure the original game files are in `game_resources/` before building
- **Build fails**: Ensure Emscripten is properly activated in your current terminal session
- **GitHub Pages not updating**: Check the Actions tab for build errors

## Notes

- The game requires the original game resource files which are **not included** in this repository due to copyright
- You can obtain these files from the original Windows XP installation or Full Tilt! Pinball
- First build will take longer as Emscripten downloads and caches SDL2 libraries
