## How to change the default directory for the `.wunjo` folder

If you need to change the location of the `.wunjo` folder, which stores the results of speech synthesis, deepfake video, and neural network models, follow these steps:

1. Open the directory where your application is installed.
2. Go to the `app/backend/[folders.py](https://github.com/wladradchenko/wunjo.wladradchenko.ru/blob/main/portable/src/backend/folders.py)` file.
3. Add the following line:

```python
os.environ["HOME"] = "path to the desired drive or folder"
```

Here `"path to the desired drive or folder"` is the location where you want to move the `.wunjo` folder.

**Note:** Make sure the specified path exists and that you have write access to this directory.