# liblvgl

LVGL (Light and Versatile Graphics Library) is a free and open-source graphics library that provides everything you need to create visually appealing and high-performance user interfaces on embedded devices.

## Description

This project packages the LVGL library version 9.2.2 for installation and use on Linux-based systems. It includes custom patches to improve compatibility and functionality.

## Requirements

- `libdrm`
- `libinput`
- `libxkbcommon`
- `ffmpeg`
- `cmake`
- `pkgconfig`
- `git`
- `SDL2`
- `ffmpeg-dev`

## Installation

To build and install the library manually, follow these steps:

1. Clone the repository and navigate to the project directory:
    ```sh
    git clone https://github.com/serper/liblvgl.git
    cd liblvgl
    ```

2. Download the sources and apply the patches:
    ```sh
    wget https://github.com/lvgl/lvgl/archive/refs/tags/v9.2.2.tar.gz -O liblvgl-9.2.2.tar.gz
    tar -xzf liblvgl-9.2.2.tar.gz
    cp lv_conf.h lvgl-9.2.2/
    patch -p1 < fix-CMakeLists.txt.patch
    patch -p1 < fix-custom.cmake.patch
    patch -p1 < fix-lv_blend_neon.S.patch
    ```

3. Build and install the library:
    ```sh
    mkdir build
    cd build
    cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON -DCMAKE_INSTALL_PREFIX=/usr -DLV_CONF_BUILD_DISABLE_DEMOS=0 -DLV_CONF_BUILD_DISABLE_EXAMPLES=0 ..
    make -j8
    sudo make install
    ```

## Creating the APK package for Alpine Linux

To create the APK package for Alpine Linux, follow these steps:

1. Clone the repository and navigate to the project directory:
    ```sh
    git clone https://github.com/serper/liblvgl.git
    cd liblvgl
    ```

2. Ensure you have `abuild` installed and configured on your system.

3. Run the following commands in the project directory:
    ```sh
    abuild checksum
    abuild -r
    ```

## Creating the Windows Package with MSYS2

To create the Windows package using `makepkg` for MSYS2, follow these steps:

1. Install MSYS2 from [msys2.org](https://www.msys2.org/) and update the package database:
    ```sh
    pacman -Syu
    ```

2. Install the necessary build tools:
    ```sh
    pacman -S base-devel mingw-w64-x86_64-toolchain git
    ```

3. Clone the repository and navigate to the project directory:
    ```sh
    git clone https://github.com/serper/liblvgl.git
    cd liblvgl
    ```

4. Build the package:
    ```sh
    makepkg -si
    ```

## Usage

After installation, you can include LVGL in your C/C++ project and start developing graphical interfaces.

## Contributions

Contributions are welcome. Please open an issue or a pull request on GitHub.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Maintainer

- Sergio Perez ([serper](https://github.com/serper))

## Links

- [LVGL Website](https://lvgl.io)
- [LVGL GitHub Repository](https://github.com/lvgl/lvgl)