### Install Wunjo AI

You can download installers for Windows, MacOS and Ubuntu operating systems on the official website [Wunjo AI](https://wladradchenko.ru/wunjo).

#### Installation on Windows

🎥 A detailed video guide for installing on Windows is available [here](https://www.youtube.com/watch?v=UzpEcPhSDrk).

All dependencies, including the ffmpeg library, will be installed automatically for Windows. However, if you want to do a manual installation, then you can download ffmpeg - [from the official website](https://ffmpeg.org/download.html), then add the path to the environment variable:
```
setx PATH "%PATH%;C:\path\to\ffmpeg\bin"
```

Installer
```
wunjo_{vesrion}.msi
```

Files for testing speech synthesis and creating deepfake videos in [GitHub Example](https://raw.githubusercontent.com/wladradchenko/wunjo.wladradchenko.ru/main/example).

Attention! When you first launch speech or video synthesis, the necessary models are downloaded, for this reason you must allow the application to connect to the network if you receive a message from the firewall. You can also install all models manually as stated in the documentation - [GitHub Wiki](https://github.com/wladradchenko/wunjo.wladradchenko.ru/wiki).

The build only works on CPU if you want to use GPU To speed up the processing process several times, visit the documentation [GitHub Wiki](https://github.com/wladradchenko/wunjo.wladradchenko.ru/wiki).

If you have problems creating deepfakes, most likely the models do not have read permissions, then you need to go to the .wunjo directory, open the console and enter:

```
icacls * /grant:r "Users:(R,W)" /T
```

Attention! Check what is installed on your computer [Visual Studio.](https://visualstudio.microsoft.com/) Because for dlib to work correctly, drivers from Visual Studio are required, which are usually preinstalled by default in Windows.

Deleting cache
```
%USERPROFILE%/.wunjo
```

#### Installation on Ubuntu

To create animation you will need to install ffmpeg
```
sudo apt install ffmpeg
```

Installing the application
```
sudo dpkg -i wunjo_{vesrion}.deb
```

Files for testing speech synthesis and creating deepfake videos in [GitHub Example](https://raw.githubusercontent.com/wladradchenko/wunjo.wladradchenko.ru/main/example).

Attention! When you first start speech or video synthesis, the necessary models are downloaded; this may take some time. You can also install all models manually as stated in the documentation - [GitHub Wiki](https://github.com/wladradchenko/wunjo.wladradchenko.ru/wiki).

If you have problems switching to GPU, read the documentation on how to install drivers [CUDA](https://github.com/wladradchenko/wunjo.wladradchenko.ru/wiki).

Uninstalling an application
```
sudo dpkg -r wunjo
```

Deleting cache
```
rm -rf ~/.wunjo
```

#### Installation on MacOS

To create animation you will need to install ffmpeg
```
brew install ffmpeg 
```

Due to the fact that the author of the project does not have an Apple license, there is currently no way to create an official installer. See [Launch project from GitHub](https://github.com/wladradchenko/wunjo.wladradchenko.ru/wiki/How-to-install-the-application#launch-project-from-github). You will need to install Git, Python3.10.

You will find detailed installation instructions in README.md or documentation.It is worth noting that on MacOS the application will only work on the CPU, since it is not supported on MacOS drivers CUDA.

Deleting cache
```
rm -rf ~/.wunjo
```

#### Launch project from GitHub

Requires 3.10 = [Python](https://www.python.org/downloads/) and [ffmpeg](https://ffmpeg.org/download.html).

Download project from GitHub manually or use git clone:

```
git clone https://github.com/wladradchenko/wunjo.wladradchenko.ru.git
```

Go to project folder:
```
cd wunjo.wladradchenko.ru
```

Create a virtual environment and activate:

```
python -m venv venv
source venv/bin/activate
```

Install dependencies:

```
// CPU
pip install -r requirements_cpu.txt  // Not MacOS
// CPU only MacOS
pip install -r requirements_macos.txt
// GPU
pip install -r requirements_gpu.txt  // Not MacOS
```

In order to use GPU you need to install CUDA 11.8. [How to use the GPU in the application](https://github.com/wladradchenko/wunjo.wladradchenko.ru/wiki/How-to-use-the-GPU-in-the-application).

You need to change to the portable directory to use the briefcase:
```
cd portable
```

Copy `pyproject.toml` for using version:
```
// CPU
cp pyproject_cpu.toml pyproject.toml
// GPU
cp pyproject_gpu.toml pyproject.toml  // Not work for MacOS
```

Run:
```
briefcase dev
```

Additionally, you can create a build to launch from file:
```
briefcase build
```

Run build
```
briefcase run
```

To create an installer:
```
briefcase package
```

More details in the BeeWare [documentation](https://beeware.org/project/projects/tools/briefcase)