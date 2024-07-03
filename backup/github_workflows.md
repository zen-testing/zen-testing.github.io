---
title: 'Github workflows 写法'
date: 2024-06-19 10:24:50
tags: [GitHub]
published: true
hideInList: false
feature: 
isTop: false
---
# 发布一个release

```yml
      - name: release
        run: |
          time_var=$(date +"%Y%m%d-%H%M%S")
          gh release create $time_var --generate-notes
          gh release upload $time_var ${{ github.workspace }}/whisper.tar.xz
        env:
          GH_TOKEN: ${{ github.token }}
        shell: bash
```

### 完整示例

```yml
# .github/workflows/release.yml
name: xz_releaser

on:
  pull_request:
  push:
    # run only against tags
    tags:
      - "xz*"
    # branches: [ "master" ]

permissions:
  contents: write
  # packages: write
  # issues: write

jobs:
  free-disk-space:
    runs-on: ubuntu-latest
    steps:
      - name: Free Disk Space (Ubuntu)
        uses: jlumbroso/free-disk-space@main
        with:
          # this might remove tools that are actually needed,
          # if set to "true" but frees about 6 GB
          tool-cache: false

          # all of these default to true, but feel free to set to
          # "false" if necessary for your workflow
          android: true
          dotnet: true
          haskell: true
          large-packages: true
          docker-images: false
          swap-storage: true
  dockerbuilder:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: go
        run: go build -o srt main.go
      - name: pwd
        run: pwd
      - name: build
        run: docker build -t whisper:latest ${{ github.workspace }}
      - name: saveSpace
        run: rm -rf /opt/hostedtoolcache
      - name: export
        run: docker save whisper:latest | xz --threads=0 -9e --memlimit-compress=0 > whisper.tar.xz
      - name: check
        run: ls -ahl ${{ github.workspace }}
      - name: Upload
        uses: actions/upload-artifact@v4
        with:
          name: xz
          path: ${{ github.workspace }}/whisper.tar.xz
          compression-level: 9 # max compression
      - name: release
        run: |
          time_var=$(date +"%Y%m%d-%H%M%S")
          gh release create $time_var --generate-notes
          gh release upload $time_var ${{ github.workspace }}/whisper.tar.xz
        env:
          GH_TOKEN: ${{ github.token }}
        shell: bash
```

# 发布一套完整的GoRelease

```yml
      - name: Run GoReleaser
        uses: goreleaser/goreleaser-action@v5
        with:
          # either 'goreleaser' (default) or 'goreleaser-pro'
          distribution: goreleaser
          version: latest
          args: release --clean
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          # Your GoReleaser Pro key, if you are using the 'goreleaser-pro' distribution
          # GORELEASER_KEY: ${{ secrets.GORELEASER_KEY }}
```

### 完整示例

```yml
# .github/workflows/release.yml
name: goreleaser

on:
  pull_request:
  push:
    # run only against tags
    tags:
      - "v*"

permissions:
  contents: write
  # packages: write
  # issues: write

jobs:
  goreleaser:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: Set up Go
        uses: actions/setup-go@v5
        with:
          go-version: stable
      # More assembly might be required: Docker logins, GPG, etc.
      # It all depends on your needs.
      - name: Run GoReleaser
        uses: goreleaser/goreleaser-action@v5
        with:
          # either 'goreleaser' (default) or 'goreleaser-pro'
          distribution: goreleaser
          version: latest
          args: release --clean
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          # Your GoReleaser Pro key, if you are using the 'goreleaser-pro' distribution
          # GORELEASER_KEY: ${{ secrets.GORELEASER_KEY }}
      - name: Upload Build Artifacts
        uses: actions/upload-artifact@v4
        with:
          name: workspace_artifacts
          path: ${{ github.workspace }}
```

# 节省空间

```yml
      - name: saveSpace
        run: rm -rf /opt/hostedtoolcache
```

### 完整示例

```yml
# .github/workflows/release.yml
name: tar_releaser

on:
  pull_request:
  push:
    # run only against tags
    tags:
      - "tar*"
    # branches: [ "master" ]

permissions:
  contents: write
  # packages: write
  # issues: write

jobs:
  dockerbuilder:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: go
        run: go build -o srt main.go
      - name: pwd
        run: pwd
      - name: build
        run: docker build -t whisper:latest ${{ github.workspace }}
      - name: saveSpace
        run: rm -rf /opt/hostedtoolcache
      - name: export
        run: docker save whisper:latest -o whisper.tar
#      - name: coreutils
#        run : apt install -y coreutils
      - name: split
        run: split -n l/10 whisper.tar whisper_part_
        # cat archive_part_* > combined.tar
      # More assembly might be required: Docker logins, GPG, etc.
      # It all depends on your needs.
      - name: check
        run : ls -ahl ${{ github.workspace }}
      - name: Upload aa
        uses: actions/upload-artifact@v4
        with:
          name: aa
          path: ${{ github.workspace }}/whisper_part_aa
          compression-level: 9 # max compression
      - name: Upload ab
        uses: actions/upload-artifact@v4
        with:
          name: ab
          path: ${{ github.workspace }}/whisper_part_ab
          compression-level: 9 # max compression
      - name: Upload ac
        uses: actions/upload-artifact@v4
        with:
          name: ac
          path: ${{ github.workspace }}/whisper_part_ac
          compression-level: 9 # max compression
      - name: Upload ad
        uses: actions/upload-artifact@v4
        with:
          name: ad
          path: ${{ github.workspace }}/whisper_part_ad
          compression-level: 9 # max compression
      - name: Upload ae
        uses: actions/upload-artifact@v4
        with:
          name: ae
          path: ${{ github.workspace }}/whisper_part_ae
          compression-level: 9 # max compression
      - name: Upload af
        uses: actions/upload-artifact@v4
        with:
          name: af
          path: ${{ github.workspace }}/whisper_part_af
          compression-level: 9 # max compression
      - name: Upload ag
        uses: actions/upload-artifact@v4
        with:
          name: ag
          path: ${{ github.workspace }}/whisper_part_ag
          compression-level: 9 # max compression
      - name: Upload ah
        uses: actions/upload-artifact@v4
        with:
          name: ah
          path: ${{ github.workspace }}/whisper_part_ah
          compression-level: 9 # max compression
      - name: Upload ai
        uses: actions/upload-artifact@v4
        with:
          name: ai
          path: ${{ github.workspace }}/whisper_part_ai
          compression-level: 9 # max compression
      - name: Upload aj
        uses: actions/upload-artifact@v4
        with:
          name: aj
          path: ${{ github.workspace }}/whisper_part_aj
          compression-level: 9 # max compression

```

# 保存工件

```yml
      - name: Upload aa
        uses: actions/upload-artifact@v4
        with:
          name: aa
          path: ${{ github.workspace }}/whisper_part_aa
          compression-level: 9 # max compression
```

# 完整示例

```yml
# .github/workflows/release.yml
name: tar_releaser

on:
  pull_request:
  push:
    # run only against tags
    tags:
      - "tar*"
    # branches: [ "master" ]

permissions:
  contents: write
  # packages: write
  # issues: write

jobs:
  dockerbuilder:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: go
        run: go build -o srt main.go
      - name: pwd
        run: pwd
      - name: build
        run: docker build -t whisper:latest ${{ github.workspace }}
      - name: saveSpace
        run: rm -rf /opt/hostedtoolcache
      - name: export
        run: docker save whisper:latest -o whisper.tar
#      - name: coreutils
#        run : apt install -y coreutils
      - name: split
        run: split -n l/10 whisper.tar whisper_part_
        # cat archive_part_* > combined.tar
      # More assembly might be required: Docker logins, GPG, etc.
      # It all depends on your needs.
      - name: check
        run : ls -ahl ${{ github.workspace }}
      - name: Upload aa
        uses: actions/upload-artifact@v4
        with:
          name: aa
          path: ${{ github.workspace }}/whisper_part_aa
          compression-level: 9 # max compression
      - name: Upload ab
        uses: actions/upload-artifact@v4
        with:
          name: ab
          path: ${{ github.workspace }}/whisper_part_ab
          compression-level: 9 # max compression
      - name: Upload ac
        uses: actions/upload-artifact@v4
        with:
          name: ac
          path: ${{ github.workspace }}/whisper_part_ac
          compression-level: 9 # max compression
      - name: Upload ad
        uses: actions/upload-artifact@v4
        with:
          name: ad
          path: ${{ github.workspace }}/whisper_part_ad
          compression-level: 9 # max compression
      - name: Upload ae
        uses: actions/upload-artifact@v4
        with:
          name: ae
          path: ${{ github.workspace }}/whisper_part_ae
          compression-level: 9 # max compression
      - name: Upload af
        uses: actions/upload-artifact@v4
        with:
          name: af
          path: ${{ github.workspace }}/whisper_part_af
          compression-level: 9 # max compression
      - name: Upload ag
        uses: actions/upload-artifact@v4
        with:
          name: ag
          path: ${{ github.workspace }}/whisper_part_ag
          compression-level: 9 # max compression
      - name: Upload ah
        uses: actions/upload-artifact@v4
        with:
          name: ah
          path: ${{ github.workspace }}/whisper_part_ah
          compression-level: 9 # max compression
      - name: Upload ai
        uses: actions/upload-artifact@v4
        with:
          name: ai
          path: ${{ github.workspace }}/whisper_part_ai
          compression-level: 9 # max compression
      - name: Upload aj
        uses: actions/upload-artifact@v4
        with:
          name: aj
          path: ${{ github.workspace }}/whisper_part_aj
          compression-level: 9 # max compression

```

# 发布本地的一个Dockerfile

```yml
name: Publish Docker Image
on:
  push:
    tags:
      - 'v*'
  workflow_dispatch:
jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - name: Extract Docker metadata
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: zhangyiming748/multimedia_processing_pipeline
      - name: Build and push Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
          platforms: |
            linux/amd64
            linux/arm64
```

# 检测当前容器所在的地区

```yml
name: Get Regions
on:
  push:
    branches:
      - dev
  workflow_dispatch:
jobs:
  GetRegions:
    runs-on: ubuntu-latest
    steps:
      - name: curl
        run: |
          curl cip.cc
          cat /etc/apt/sources.list
          ls /etc/apt/sources.list.d
```

# 发布一个go release版本

```yml
# .github/workflows/GoRelease.yml
name: goreleaser

on:
  pull_request:
  push:
    # run only against tags
    tags:
      - "v*"

permissions:
  contents: write
  # packages: write
  # issues: write

jobs:
  goreleaser:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: Set up Go
        uses: actions/setup-go@v5
        with:
          go-version: stable
      # More assembly might be required: Docker logins, GPG, etc.
      # It all depends on your needs.
      - name: Run GoReleaser
        uses: goreleaser/goreleaser-action@v5
        with:
          # either 'goreleaser' (default) or 'goreleaser-pro'
          distribution: goreleaser
          version: latest
          args: release --clean
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          # Your GoReleaser Pro key, if you are using the 'goreleaser-pro' distribution
          # GORELEASER_KEY: ${{ secrets.GORELEASER_KEY }}
      - name: Upload Build Artifacts
        uses: actions/upload-artifact@v4
        with:
          name: workspace_artifacts
          path: ${{ github.workspace }}
```

# 自动发布当前代码仓库

```yml
name: ci

on:
  push:
    branches:
      - master
  schedule:
    - cron: "0 */4 * * *"

jobs:
  autogreen:
    runs-on: ubuntu-latest
    steps:
      - name: Clone repository
        uses: actions/checkout@v2

      - name: Auto green
        run: |
          git config --local user.email "zhangyiming748@gmail.com"
          git config --local user.name "zen"
          git remote set-url origin https://${{ github.actor }}:${{ secrets.GITHUB_TOKEN }}@github.com/${{ github.repository }}
          git pull --rebase
          git commit --allow-empty -m "a commit a day keeps your girlfriend away"
          git push
```

# 保存工件

```yml
# .github/workflows/release.yml
name: xz_releaser

on:
  pull_request:
  push:
    # run only against tags
    tags:
      - "xz*"
    # branches: [ "master" ]

permissions:
  contents: write
  # packages: write
  # issues: write

jobs:
  dockerbuilder:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - name: build
        run: docker build -t convertimage:latest ${{ github.workspace }}
      - name: saveSpace
        run: rm -rf /opt/hostedtoolcache
      - name: export
        run: docker save ConvertImage:latest | xz --threads=0 -9e --memlimit-compress=0 > ConvertImage.tar.xz
      - name: Upload
        uses: actions/upload-artifact@v4
        with:
          name: ConvImage.tar.xz
          path: ${{ github.workspace }}/ConvertImage.tar.xz
          compression-level: 9 # max compression
```

# 使用gh发布release

```yml
name: Docker Installer Download

on:
  workflow_dispatch: # 表示该workflow可以通过手动触发。在GitHub仓库中，你可以看到一个"Run workflow"按钮，点击后可以手动运行这个workflow
#  schedule: # 表示该workflow可以通过定时任务触发。在这个例子中，定时任务的时间表达式为00 23 * * *，表示每天的23点0分执行一次
#    - cron: '00 23 * * *'
  push:
    tags:
      - "docker*"
permissions:
  contents: write
jobs:
  download_installer:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      - name: Download installers
        run: |
          curl -o linux.sh "https://get.docker.com"
          curl -o docker_desktop_installer_windows_x86_64.exe "https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe"
          curl -o docker_desktop_installer_mac_arm64.dmg "https://desktop.docker.com/mac/main/arm64/Docker.dmg"
          curl -o docker_desktop_installer_mac_x84_64.dmg "https://desktop.docker.com/mac/main/amd64/Docker.dmg"
          curl -o docker_desktop_installer_linux_debian_x84_64.dmg "https://desktop.docker.com/linux/main/amd64/149282/docker-desktop-4.30.0-amd64.deb"
          curl -o docker_desktop_installer_linux_fedora_x84_64.dmg "https://desktop.docker.com/linux/main/amd64/149282/docker-desktop-4.30.0-x86_64.rpm"
      - name: Release
        uses: softprops/action-gh-release@v2
        with:
          files: |
            linux.sh
            docker_desktop_installer_windows_x86_64.exe
            docker_desktop_installer_mac_arm64.dmg
            docker_desktop_installer_mac_x84_64.dmg
            docker_desktop_installer_linux_debian_x84_64.dmg
            docker_desktop_installer_linux_fedora_x84_64.dmg
          tag_name: latest_release
      - name: ls
        run: ls ${{ github.workspace }}
      - name: Upload Build Artifacts
        uses: actions/upload-artifact@v4
        with:
          name: Docker installers
          path: ${{ github.workspace }}
```