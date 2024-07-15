![alt text][logo]

[logo]:https://github.com/Miku-UI/manifesto/blob/Udon_v2/img/MikuUI.png "Miku-UI Android"

### To get started with building Miku-UI GSI,
you'll need to get familiar with [Git and Repo](https://source.android.com/source/using-repo.html)

### Official Channel
[Channel](https://t.me/mikutreblebuilds)

[Support chat](https://t.me/mikutreblechat)

### 1.1 Installing dependencies and Repo ###

Several packages are needed in order to build crDroid
```
sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git git-lfs gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-gtk3-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```

Install Repo tool
```bash
# Make a directory where Repo will be stored and add it to the path
$ mkdir ~/bin
$ PATH=~/bin:$PATH

# Download Repo itself
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

# Make Repo executable
$ chmod a+x ~/bin/repo
```

### Create the directories

As a first step, you'll have to create and enter a folder with the appropriate name.
To do that, run these commands:

```bash
   mkdir Miku
   cd Miku
```

### To initialize your local repository, run this command:

```bash
   repo init -u https://github.com/Miku-UI/manifesto -b Udon_v2
```
 

### Clone the Manifest to add necessary dependencies for gsi:
 
    git clone https://github.com/MaloyBegonia/treble_manifest .repo/local_manifests  -b 14
  


### Afterwards, sync the source by running this command:

```bash
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune
```

## Generating Rom Makefile

 In rom folder,
 
 ```
    cd device/phh/treble
    bash generate.sh miku
 ```

## Maintainer-info
Set your maintainer name 
[Maintainer-name](https://github.com/MaloyBegonia/device_phh_treble_beta/blob/test/miku.mk#L10)

### Build vanilla variant
```
rm -rf vendor/gapps
```

### Manifest for create signed build(s)
[Manifest](https://github.com/MaloyBegonia/Miku-ui-build-signed-script)

### Turn on caching to speed up build

You can speed up subsequent builds by adding these lines to your ~/.bashrc OR ~/.zshrc file:

```
export USE_CCACHE=1
export CCACHE_COMPRESS=1
export CCACHE_MAXSIZE=50G # 50 GB
``` 

## Compilation 

In rom folder,

 ```
 . build/envsetup.sh
 ccache -M 50G -F 0
 lunch treble_arm64_bgN-ap2a-userdebug 
 make systemimage -j$(nproc --all)
 ```


## Compress

After compilation,
If you want to compress the build.
In rom folder,

   ```
        cd out/target/product/tdgsi_arm64_ab
        xz -z -k system.img 
   ```
