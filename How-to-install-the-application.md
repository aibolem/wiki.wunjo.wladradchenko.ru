### Install Wunjo AI

You can download installers for Windows, MacOS and Ubuntu operating systems on the official website [Wunjo AI](wladradchenko.ru/wunjo).

#### Installation on Windows

🎥 A detailed video guide for installing on Windows is available [here](https://youtu.be/2qIpJYhOL2U).

```bash
# To create animation, you need to install ffmpeg and add it to system variables
setx PATH "%PATH%;C:\path\to\ffmpeg\bin"

# Run the installer
wunjo_{version}.msi

# Important! When you first start speech synthesis, video (individual functions that you have not previously run), models will be downloaded in size (~ 1-5 GB). This may take time.
# Please note that if you have a firewall active, it may block the download. Download models manually.

# Setting permissions for deepfake
icacls "%USERPROFILE%/.wunjo/deepfake/gfpgan/weights/*.pth" /grant:r "Users":(R,W)

# Clear cache
%USERPROFILE%/.wunjo
```

#### Installation on Ubuntu

```bash
# Installing the necessary component to create animation
sudo apt install ffmpeg

# Run the installer
sudo dpkg -i wunjo_{version}.deb

# Important! Models (~5 GB) will be downloaded the first time video synthesis is started.

# Delete app and cache
sudo dpkg -r wunjo
rm -rf ~/.wunjo
```

#### Installation on MacOS

```bash
# Installing the necessary component to create animation
brew install ffmpeg

# Unzip the application
unzip wunjo_macos_{version}.zip

# Important! Models (~5 GB) will be downloaded the first time video synthesis is started.

# Clear cache
rm -rf ~/.wunjo
```

#### Launch project from GitHub

Requires 3.8 <= [Python](https://www.python.org/downloads/) <=3.10 and [ffmpeg](https://ffmpeg.org/download.html).

Create a virtual environment and activate:

```
python -m venv venv
source venv/bin/activate
```

Install dependencies:

```
pip install -r requirements.txt
```

Attention! The first time you run video synthesis, models will be downloaded in .wunjo/deepfake in the amount of 1-5GB, depending on the function being launched. This may take a long time. For speech synthesis, models will also be downloaded when you first start voice or voice clone.

You need to change to the portable directory to use the briefcase:
```
cd portable
```

Run:
```
brief case dev
```

Additionally, you can create a build
```
brief case build
```

Run build
```
brief case run
```

To create an installer:
```
brief case package
```

More details in the BeeWare [documentation](https://beeware.org/project/projects/tools/briefcase)