# Biblioteca FFmpeg

## Descripción
Este proyecto compila la biblioteca FFmpeg desde el código fuente con parches y configuraciones específicas. Optimizado para Allwinner T113-S3 con decodificación acelerada por hardware.

## Instrucciones de Construcción
1. Clonar el repositorio:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```
2. Descargar el código fuente y los parches:
    ```sh
    wget https://github.com/FFmpeg/FFmpeg/archive/refs/heads/release/7.1.zip
    wget <patch-urls>
    ```
3. Construir el proyecto:
    ```sh
    abuild -r
    ```

## Instalación
Después de construir, el paquete se puede instalar usando:
```sh
    sudo apk add --allow-untrusted <package-name>.apk