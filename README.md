# GitHub Actions Workflows for Godot Engine projects

This repository contains useful GitHub Actions workflow files for Godot Engine projects, namely:

- The `build-game-<version>.yml` files, which can build your game for all platforms, upload artifacts and publish it to HTML5 on a `gh-pages` branch.

## How to use

Here is an example using the `build-game-3.5.yml` workflow (= build a game using Godot Engine 3.5).

In your repository, let's create a workflow named `push.yml` in the `.github/workflows` directory.  
The following code is extracted from my game [Deep Space Beat](https://github.com/Srynetix/deep-space-beat/), so don't forget to change the game `name` and `output_name` on each job.

```yaml
name: Push builds

on:
  push:
    branches:
      - main

jobs:
  build-web:
    uses: Srynetix/godot-github-workflows/.github/workflows/build-game-3.5.yml@main
    with:
      platform: HTML5
      name: deep-space-beat
      output_name: index.html
  build-windows:
    uses: Srynetix/godot-github-workflows/.github/workflows/build-game-3.5.yml@main
    with:
      platform: Windows Desktop
      name: deep-space-beat
      output_name: Deep Space Beat.exe
  build-mac:
    uses: Srynetix/godot-github-workflows/.github/workflows/build-game-3.5.yml@main
    with:
      platform: Mac OSX
      name: deep-space-beat
      output_name: Deep Space Beat.zip
  build-linux:
    uses: Srynetix/godot-github-workflows/.github/workflows/build-game-3.5.yml@main
    with:
      platform: Linux X11
      name: deep-space-beat
      output_name: Deep Space Beat.x86_64
  build-android-debug:
    uses: Srynetix/godot-github-workflows/.github/workflows/build-game-3.5.yml@main
    with:
      platform: Android
      name: deep-space-beat
      output_name: Deep Space Beat.apk
      debug: true
```

Here's what the workflow is doing:

> On each `push` on the `main` branch, it will export the project for the Web, Windows, macOS, Linux and Android (debug mode) targets.

You can remove the platforms you don't want to support, and make sure the corresponding export configurations exist in your game.

For a short example, if you only need so push your game on GitHub Pages (so only build the HTML5 target), and your game is named "Sample", you can use the following code:

```yaml
name: Push builds

on:
  push:
    branches:
      - main

jobs:
  build-web:
    uses: Srynetix/godot-github-workflows/.github/workflows/build-game-3.5.yml@main
    with:
      platform: HTML5
      name: sample
      output_name: index.html
```