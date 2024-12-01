# liblvgl

LVGL (Light and Versatile Graphics Library) es una biblioteca gráfica gratuita y de código abierto que proporciona todo lo necesario para crear interfaces de usuario visualmente atractivas y de alto rendimiento en dispositivos embebidos.

## Descripción

Este proyecto empaqueta la biblioteca LVGL versión 9.2.2 para su instalación y uso en sistemas basados en Linux. Incluye parches personalizados para mejorar la compatibilidad y funcionalidad.

## Requisitos

- `libdrm`
- `libinput`
- `libxkbcommon`
- `ffmpeg`
- `cmake`
- `pkgconfig`
- `git`
- `ffmpeg-dev`

## Instalación

Para compilar e instalar la biblioteca de forma manual, siga estos pasos:

1. Clone el repositorio y navegue al directorio del proyecto:
    ```sh
    git clone https://github.com/serper/liblvgl.git
    cd liblvgl
    ```

2. Descargue las fuentes y aplique los parches:
    ```sh
    wget https://github.com/lvgl/lvgl/archive/refs/tags/v9.2.2.tar.gz -O liblvgl-9.2.2.tar.gz
    tar -xzf liblvgl-9.2.2.tar.gz
    cp lv_conf.h lvgl-9.2.2/
    patch -p1 < fix-CMakeLists.txt.patch
    patch -p1 < fix-custom.cmake.patch
    patch -p1 < fix-lv_blend_neon.S.patch
    ```

3. Compile e instale la biblioteca:
    ```sh
    mkdir build
    cd build
    cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON -DCMAKE_INSTALL_PREFIX=/usr -DLV_CONF_BUILD_DISABLE_DEMOS=0 -DLV_CONF_BUILD_DISABLE_EXAMPLES=0 ..
    make -j8
    sudo make install
    ```

## Creación del paquete APK para Alpine Linux

Para crear el paquete APK para Alpine Linux, siga estos pasos:

1. Clone el repositorio y navegue al directorio del proyecto:
    ```sh
    git clone https://github.com/serper/liblvgl.git
    cd liblvgl
    ```

2. Asegúrese de tener `abuild` instalado y configurado en su sistema.

3. Ejecute los siguientes comandos en el directorio del proyecto:
    ```sh
    abuild checksum
    abuild -r
    ```

## Uso

Después de la instalación, puede incluir LVGL en su proyecto C/C++ y comenzar a desarrollar interfaces gráficas.

## Contribuciones

Las contribuciones son bienvenidas. Por favor, abra un issue o un pull request en GitHub.

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulte el archivo `LICENSE` para más detalles.

## Mantenedor

- Sergio Perez ([serper](https://github.com/serper))

## Enlaces

- [Sitio web de LVGL](https://lvgl.io)
- [Repositorio de GitHub de LVGL](https://github.com/lvgl/lvgl)
