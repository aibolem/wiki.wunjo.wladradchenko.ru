# Troubleshooting "File is too big" Message

When launching a specific module, you might encounter the "File is too big" message. This could indicate an issue with file loading into the `.wunjo/tmp` directory. This problem could stem from browser peculiarities or memory cache limitations. If you've encountered this problem, you may need to adjust the file loading time to suit your needs.

To customize the file loading time, open the file [general_utils.py](https://github.com/wladradchenko/wunjo.wladradchenko.ru/blob/main/portable/src/backend/general_utils.py) and locate the `check_tmp_file_uploaded` method. You can modify the parameters within this method:

```python
def check_tmp_file_uploaded(file_path, retries=10, delay=30):
    """
    Checks for the existence of a file with a specified number of attempts and a delay between attempts.

    :param file_path: Path to the file to check.
    :param retries: Number of attempts.
    :param delay: Delay in seconds between attempts.
    :return: True if the file exists, False otherwise.
    """
    for _ in range(retries):
        if os.path.exists(file_path):
            return True
        time.sleep(delay)
    return False
```

In this code, `retries` refer to the number of attempts to check file upload to `.wunjo/tmp`, while `delay` signifies the waiting time between each attempt.

Utilize these parameters to tailor your application's behavior according to your requirements.