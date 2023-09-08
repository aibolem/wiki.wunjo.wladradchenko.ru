If automatic installation of models does not suit you for some reason, you can always download and install them manually.

1. **Go to the desired directory**:
Change to the `~/.wunjo` directory on Unix-like systems or `%USERPROFILE%/.wunjo` on Windows. This directory can also be accessed from the application by clicking on the folder icon on the left side of the screen.

    ![screenshot 1](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/7e1d14fe-62bd-4d43-a0f2-3c08eea419ca)

2. **Working with the `voice` directory**:
Voice models are stored in this directory. It also contains a file with download links for specific models.

    ![screenshot 2](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/40a7a13b-61a1-48f9-8f2e-b7bf8b82a84a)

3. **Directory content**:
Each subdirectory contains two models: Encoder and Vocoder.

    ![screenshot 3](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/c50e20b9-f33e-4e0f-b10a-baf08befd97a)

4. **Examining the `voice.json` file**:
Open the `voice.json` file and notice the structure. As an example, consider the voice of "Russian man".

**Configuration example:**

```
{
   "Russian man": {
     "avatar_download": "https://wladradchenko.ru/static/wunjo.wladradchenko.ru/avatar/Man.png",
     "checkpoint_download": "https://wladradchenko.ru/static/wunjo.wladradchenko.ru/tacotron2/checkpoint_man",
     "waveglow_download": "https://wladradchenko.ru/static/wunjo.wladradchenko.ru/waveglows/waveglow.pt",
     "voice_control_cfg": {
       "psola": {
         "max_hz": 2100,
         "min_hz": 30,
         "analysis_win_ms": 40,
         "max_change": 2.955,
         "min_change": 0.795
       },
       phase: {
         "nft": 256
         "hop": 64
       }
     },
     "user_dict": null
     "text_handler": {
       "config": "en",
       "out_max_length": 200
     },
     modules: {
       "engine": "tacotron2",
       "vocoder": "waveglow"
     },
     engine: {
       "tacotron2": {
         "model_path": "voice/man/checkpoint_man",
         "hparams_path": null,
         "options": {
           "steps_per_symbol": 10,
           gate_threshold: 0.5
         }
       }
     },
     "vocoder": {
       waveglow: {
         "model_path": "voice/man/waveglow_man.pt",
         "options": {
           "sigma": 0.666,
           "strength": 0.1
         }
       }
     }
   }
}
```

5. **Model Download Links**:
In the configuration file you will find links to download models.

    - Encoder: `"checkpoint_download": "https://wladradchenko.ru/static/wunjo.wladradchenko.ru/tacotron2/checkpoint_man"`
    - Vocoder: `"waveglow_download": "https://wladradchenko.ru/static/wunjo.wladradchenko.ru/waveglows/waveglow.pt"`

6. **Download and file location**:
Download the models and place them in the appropriate directories. Please note that the files must be in their original format, not unpacked. If Windows automatically converts files to folders, return them to their original state (for example, by zipping and renaming the extension).

    - For the `checkpoint_man` model, you can see from the path that you need to create a `man` subdirectory and place a file called `checkpoint_man` there: `"model_path": "voice/man/checkpoint_man`
    - For the `waveglow.pt` model, you can see from the path that you need to create a `man` subdirectory, but rename the file to `waveglow_man.pt` before placing it: `"model_path": "voice/man/waveglow_man.pt"`

Similarly, you can work with other voices. Now you know how to manually install voice models.