# dockle-action

This is unofficial GitHub Action for [goodwithtech/dockle](https://github.com/goodwithtech/dockle). It provides minimal functionality. For example, it does not support `--input` or options related to container registry.

## Usage

```yml
name: Build
on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Set image tag
        id: build
        run: |
          echo '::set-output name=image_tag::docker.io/my-org/my-app:${{ github.sha }}'
      - name: Build an image from Dockerfile
        run: |
          docker build -t ${{ steps.build.outputs.image_tag }} .
      - name: Run Dockle
        uses: nemotoy/dockle-action@main
        with:
          image: ${{ steps.build.outputs.image_tag }}
          exit-code: '1'
          exit-level: WARN
```
