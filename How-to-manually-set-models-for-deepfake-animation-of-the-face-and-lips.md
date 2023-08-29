If automatic installation of models does not suit you for some reason, you can always download and install them manually.

1. **Go to the desired directory**:
Change to the `~/.wunjo` directory on Unix-like systems or `%USERPROFILE%/.wunjo` on Windows. This directory can also be accessed from the application by clicking on the folder icon on the left side of the screen.

![screenshot 1](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/7e1d14fe-62bd-4d43-a0f2-3c08eea419ca)

2. **Working with the `deepfake` directory**:
Models for deepfake are stored in this directory. It also contains a file with links to download the models.

![screenshot 2](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/16187e6d-3b56-4203-b220-4a2b888cd833)

3. **Directory content**:
checkpoints directory:

![screenshot 3](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/c913d274-e84c-48bf-8efb-6f72cf8ba716)

You may notice that only two archives are unzipped: `BFM_Fitting.zip` and `hub.zip`. The rest of the models are files.

Inside `BFM_Fitting` you will find the following models:

![screenshot 4](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/d7c4f4a1-e0f3-4a33-94c2-923db54f5807)

Inside `hub/checkpoints` you will find two models:

![screenshot 5](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/1186aab7-7371-4a33-9f5e-1f467c1c773b)

Let's look at the `gfpgan/weights` directory, which is responsible for improving the quality of the face or background.

![screenshot 6](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/b4850275-a20b-49be-b0d0-5e2b3f4182e4)

It is worth noting that for Windows it will be necessary to give permissions to read models, which are found in checkpoints and in gfpgan, for example: `icacls "%USERPROFILE%/.wunjo/deepfake/path_to_model" /grant:r "Users":(R,W )`. You can see an explanation of the directories in the installation video for [Windows](https://youtu.be/2qIpJYhOL2U).

4. **Where to download models for face animation**:
You can find download links for models in `.wunjo/deepfake/deepfake.json`.

Let's see what's inside:

```
{
   "checkpoints": {
     "auido2exp_00300-model.pth": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/auido2exp_00300-model.pth",
     "auido2pose_00140-model.pth": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/auido2pose_00140-model.pth",
     "epoch_20.pth": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/epoch_20.pth",
     "facevid2vid_00189-model.pth.tar": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/facevid2vid_00189-model.pth.tar",
     "shape_predictor_68_face_landmarks.dat": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/shape_predictor_68_face_landmarks.dat",
     "wav2lip.pth": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/wav2lip.pth",
     "mapping_00229-model.pth.tar": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/mapping_00229-model.pth.tar",
     "mapping_00109-model.pth.tar": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/mapping_00109-model.pth.tar",
     "BFM_Fitting.zip": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/BFM_Fitting.zip",
     "hub.zip": "https://github.com/Winfredy/SadTalker/releases/download/v0.0.2/hub.zip",
     "s3fd.pth": "https://www.adrianbulat.com/downloads/python-fan/s3fd-619a316812.pth"
   },
   "gfpgan": {
     "alignment_WFLW_4HG.pth": "https://github.com/xinntao/facexlib/releases/download/v0.1.0/alignment_WFLW_4HG.pth",
     "detection_Resnet50_Final.pth": "https://github.com/xinntao/facexlib/releases/download/v0.1.0/detection_Resnet50_Final.pth",
     "GFPGANv1.4.pth": "https://github.com/TencentARC/GFPGAN/releases/download/v1.3.0/GFPGANv1.4.pth",
     "parsing_parsenet.pth": "https://github.com/xinntao/facexlib/releases/download/v0.2.2/parsing_parsenet.pth",
     "RestoreFormer.pth": "https://github.com/TencentARC/GFPGAN/releases/download/v1.3.4/RestoreFormer.pth",
     "codeformer.pth": "https://github.com/sczhou/CodeFormer/releases/download/v0.1.0/codeformer.pth",
     "RealESRGAN_x2plus.pth": "https://github.com/xinntao/Real-ESRGAN/releases/download/v0.2.1/RealESRGAN_x2plus.pth"
   }
}
```

As you can see, models under `checkpoints` are downloaded to the `checkpoints` directory. Models under `gfpgan` are downloaded to the `gfpgan` directory.

Now you know how to manually set models for deepfake face and lip animations.