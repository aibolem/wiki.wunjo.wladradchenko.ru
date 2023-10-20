Enhance the performance and speed of operations in the Wunjo AI application by harnessing the power of your GPU. To achieve this, you need to install NVIDIA CUDA drivers. This guide will help you with the installation process on various operating systems.

### Prerequisites

Ensure that your system meets the following requirements before installing CUDA:

- NVIDIA GPU (Kepler architecture or newer)
- A supported version of [Windows](https://developer.nvidia.com/cuda-toolkit-archive), [Ubuntu](https://developer.nvidia.com/cuda-toolkit-archive), or [macOS](https://developer.nvidia.com/cuda-toolkit-archive) (note that macOS support is limited; refer to NVIDIA’s documentation for detailed information)
- Minimum of 8GB RAM (16GB or more recommended)

### Recommended CUDA Version

For the best compatibility and performance, we recommend installing **CUDA 11.8**.

### Installation Guide

Follow the instructions below to install CUDA on your operating system:

#### Windows

1. Visit the [NVIDIA CUDA Toolkit download page](https://developer.nvidia.com/cuda-downloads) or [NVIDIA CUDA Toolkit 11.8](https://developer.nvidia.com/cuda-11-8-0-download-archive).
2. Choose the appropriate version for your system and download the installer.
3. Run the installer and follow the on-screen instructions to complete the installation.
4. Restart your system to finalize the installation.

#### Ubuntu/Debian

1. Open your terminal and update your repository and install the necessary dependencies using the following commands:

    ```bash
    sudo apt update
    sudo apt install build-essential dkms
    ```

2. Go to the [NVIDIA CUDA Toolkit download page](https://developer.nvidia.com/cuda-downloads).
3. Select "Linux" and choose the right options for your system to get the installation commands.
4. Execute the provided commands in your terminal to install CUDA.
5. Restart your system to complete the installation.

#### macOS

NVIDIA has discontinued support for CUDA on macOS from CUDA 10.2 onwards. Users with macOS are recommended to explore NVIDIA's alternatives such as OpenCL. Further details are available on the [official PyTorch page](https://pytorch.org/get-started/locally/).

### Leveraging GPU in the Wunjo AI Application

#### Windows

To use the GPU in the Wunjo AI application on Windows, you need to rebuild the build because the default is set up for CPU usage. Here is how you can set it up:

1. **Clone the project**:

    ```bash
    git clone https://github.com/wladradchenko/wunjo.wladradchenko.ru.git
    ```

2. **Ensure you have the necessary tools installed**:
   
    - [Python 3.10](https://www.python.org/downloads/)
    - [ffmpeg](https://ffmpeg.org/download.html)

3. **Set up a virtual environment**:

    ```bash
    python -m venv venv
    venv\Scripts\activate.bat
    ```

4. **Install dependencies**:

    ```
    python -m pip install --upgrade pip
    python -m pip install --upgrade setuptools
    python -m pip install --upgrade wheel
    python -m pip install -r requirements_gpu.txt
    python -m pip install torch==2.0.0+cu118 torchvision==0.15.1+cu118 --extra-index-url https://download.pytorch.org/whl/cu118
    python -m pip install xformers==0.0.19
    ```

5. **Verify CUDA installation**:
   
    After installing the torch libraries, check that CUDA has installed correctly. Open your Python environment and run the following script:
    ```
    python
    ```

    ```
    import torch

    if torch.cuda.is_available():
        print("CUDA is available")
    else:
        print("CUDA is not available")
    ```

    You should see the message "CUDA is available" if everything is set up correctly.

6. **Navigate to the portable folder**:

    ```bash
    cd portable
    ```

7. **Development mode**:
   
    To run in development mode, use the command:

    ```bash
    briefcase dev
    ```

8. **Building the application**:

    - To build:

        ```bash
        briefcase build
        ```

      Please note that on Windows the following errors may occur after the build:

      ```
      'NoneType' object has no attribute 'flush'
      ```
      To fix it, you need to remove the line `_default_handler.flush = sys.stderr.flush` in `wunjo/app/src/app_packages/transformers/utils/logging.py`.
    
      Torch after the briefcase build was installed only for the CPU. Need to copy from venv torch and torchvision and replace torch and torchvision in `wunjo/app/src/app_packages/`

    - To run:

        ```bash
        briefcase run
        ```

    - To package:

        ```bash
        briefcase package
        ```

    Note that creating a larger installer might encounter issues due to the 2GB size limit for MSI installers on Windows. Hence, we officially distribute only the CPU version for Windows.

If you are unable to build an application for the GPU, take a look at the solution to common problems [Issue 28](https://github.com/wladradchenko/wunjo.wladradchenko.ru/issues/28).

#### Ubuntu/Debian

The Ubuntu application is naturally compatible with GPU libraries. Open the application, activate the GPU switch ![Screenshot from 2023-09-07 09-55-54](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/3799f33e-f333-4340-8b78-6c73dd3a290c), and you should see a message indicating that the GPU has been activated.

![Screenshot from 2023-09-07 09-56-03](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/9b1403fd-c496-4ba9-aec2-03f35a6982a0)

#### macOS

Due to the lack of driver support on macOS, you are limited to using the CPU. However, you can modify the application for use with OpenCL alternatives.