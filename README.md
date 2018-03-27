
sudo emerge -a nheko
```

#### Alpine Linux (and postmarketOS)

Make sure you have the testing repositories from `edge` enabled. Note that this is not needed on postmarketOS.

```sh
sudo apk add nheko
```

### Build Requirements

- Qt5 (5.7 or greater). Qt 5.7 adds support for color font rendering with
  Freetype, which is essential to properly support emoji.
- CMake 3.1 or greater.
- [LMDB](https://symas.com/lightning-memory-mapped-database/).
- A compiler that supports C++11.
    - Clang 3.8 (or greater).
    - GCC 7 (or greater).

#### Linux 

If you don't want to install any external dependencies, you can generate an AppImage locally using docker.

```bash
make docker-app-image
```

If you're on Debian you should use `make docker-debian-appimage` instead, which uses
Debian as the build host in an attempt to work around this [issue](https://github.com/AppImage/AppImageKit/wiki/Desktop-Linux-Platform-Issues#openssl).

##### Arch Linux

```bash
sudo pacman -S qt5-base qt5-tools qt5-multimedia cmake gcc fontconfig lmdb
```

##### Gentoo Linux

```bash
sudo emerge -a ">=dev-qt/qtgui-5.7.1" media-libs/fontconfig
```

##### Ubuntu (e.g 14.04)

```bash
sudo add-apt-repository ppa:beineri/opt-qt592-trusty
sudo add-apt-repository ppa:george-edison55/cmake-3.x
sudo apt-get update
sudo apt-get install -y qt59base qt59tools qt59multimedia cmake liblmdb-dev
```

To build on Ubuntu 14.04 Trusty out-of-the-box requires using Clang 3.6 instead of GCC:

```bash
sudo apt-get install clang-3.6
export CC=clang-3.6 CXX=clang++-3.6
```

On Ubuntu 14.04 Trusty, it's possible to use GCC 4.9.4+, but it is not recommended, because it requires installing GCC packages from third-party PPAs.  Later versions of Ubuntu that come with GCC 4.9.4+ should work with GCC out-of-the-box.

##### macOS (Xcode 8 or later)

```bash
brew update
brew install qt5 lmdb cmake llvm
```

### Building

Clone the repo and run

```bash
make release
```

which invokes cmake and translates to

```bash
cmake -H. -Bbuild -DCMAKE_BUILD_TYPE=RelWithDebInfo
cmake --build build
```

If the build fails with the following error
```
Could not find a package configuration file provided by "Qt5Widgets" with
any of the following names:

Qt5WidgetsConfig.cmake
qt5widgets-config.cmake
```
You might need to pass `-DCMAKE_PREFIX_PATH` to cmake to point it at your qt5 install.

e.g on macOS

```
cmake -H. -Bbuild -DCMAKE_BUILD_TYPE=RelWithDebInfo -DCMAKE_PREFIX_PATH=$(brew --prefix qt5)
cmake --build build
```

The `nheko` binary will be located in the `build` directory.

#### Nix

Download the repo as mentioned above and run

```bash
nix-build
```

in the project folder. This will output a binary to `result/bin/nheko`.

You can also install nheko by running `nix-env -f . -i`

### Contributing

Any kind of contribution to the project is greatly appreciated. You are also
encouraged to open feature request issues.

### Screenshot

Here is a screenshot to get a feel for the UI, but things will probably change.

![nheko](https://dl.dropboxusercontent.com/s/a493o47obvez6v1/nheko.png)

### Third party

- [Emoji One](http://emojione.com)
- [Font Awesome](http://fontawesome.io/)
- [Open Sans](https://fonts.google.com/specimen/Open+Sans)

[Matrix](https://matrix.org)
[Riot](https://riot.im)
