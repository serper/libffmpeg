# FFmpeg Library

## English

### Description
This project builds the FFmpeg library from source with specific patches and configurations. Optimized for Allwinner T113-S3 with accelerated hardware video decoding.

### Build Instructions
1. Clone the repository:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```
2. Download the source and patches:
    ```sh
    wget https://github.com/FFmpeg/FFmpeg/archive/refs/heads/release/7.1.zip
    wget <patch-urls>
    ```
3. Build the project:
    ```sh
    abuild -r
    ```

### Installation
After building, the package can be installed using:
```sh
    sudo apk add --allow-untrusted <package-name>.apk