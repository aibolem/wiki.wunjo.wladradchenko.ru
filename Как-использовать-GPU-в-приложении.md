Улучшите производительность и скорость операций в приложении Wunjo AI, используя возможности вашего GPU. Для этого вам потребуется установить драйверы NVIDIA CUDA. Это руководство поможет вам с установкой на различных операционных системах.

### Предварительные требования

Перед установкой CUDA убедитесь, что ваша система соответствует следующим требованиям:

- Видеокарта NVIDIA (архитектура Kepler или новее)
- Поддерживаемая версия [Windows](https://developer.nvidia.com/cuda-toolkit-archive), [Ubuntu](https://developer.nvidia.com/cuda-toolkit-archive) или [macOS](https://developer.nvidia.com/cuda-toolkit-archive) (обратите внимание, что поддержка macOS ограничена; за деталями обращайтесь к документации NVIDIA)
- Минимум 8 ГБ оперативной памяти (рекомендуется 16 ГБ или больше)

### Рекомендуемая версия CUDA

Для лучшей совместимости и производительности рекомендуем установить **CUDA 11.8**.

### Руководство по установке

Следуйте инструкциям ниже для установки CUDA на вашу операционную систему:

#### Windows

1. Перейдите на [страницу загрузки NVIDIA CUDA Toolkit](https://developer.nvidia.com/cuda-downloads) или [NVIDIA CUDA Toolkit 11.8](https://developer.nvidia.com/cuda-11-8-0-download-archive).
2. Выберите соответствующую версию для вашей системы и загрузите установщик.
3. Запустите установщик и следуйте инструкциям на экране для завершения установки.
4. Перезагрузите систему, чтобы завершить установку.

#### Ubuntu/Debian

1. Откройте терминал и обновите репозиторий, а затем установите необходимые зависимости с помощью следующих команд:

    ```bash
    sudo apt update
    sudo apt install build-essential dkms
    ```

2. Перейдите на [страницу загрузки NVIDIA CUDA Toolkit](https://developer.nvidia.com/cuda-downloads).
3. Выберите "Linux" и выберите подходящие параметры для вашей системы, чтобы получить команды для установки.
4. Выполните предоставленные команды в терминале для установки CUDA.
5. Перезагрузите систему, чтобы завершить установку.

#### macOS

К сожалению, NVIDIA прекратила поддержку CUDA на macOS, начиная с версии CUDA 10.2. Пользователям с macOS рекомендуется рассмотреть альтернативы NVIDIA, такие как OpenCL. Подробности можно найти на [официальной странице PyTorch](https://pytorch.org/get-started/locally/).

### Использование GPU в приложении Wunjo AI

#### Windows

Чтобы использовать GPU в приложении Wunjo AI на Windows, вам нужно пересобрать сборку, потому что по умолчанию она настроена на работу с CPU. Вот как вы можете это настроить:

1. **Клонируйте проект**:

    ```bash
    git clone https://github.com/wladradchenko/wunjo.wladradchenko.ru.git
    ```

2. **Убедитесь, что у вас установлены необходимые инструменты**:
   
    - [Python 3.10](https://www.python.org/downloads/)
    - [ffmpeg](https://ffmpeg.org/download.html)

3. **Настройка виртуальной среды**:

    ```bash
    python -m venv venv
    venv\Scripts\activate.bat
    ```

4. **Установка зависимостей**:

    ```
    python -m pip install --upgrade pip
    python -m pip install --upgrade setuptools
    python -m pip install --upgrade wheel
    python -m pip install -r requirements_gpu.txt
    python -m pip install torch==2.0.0+cu118 torchvision==0.15.1+cu118 --extra-index-url https://download.pytorch.org/whl/cu118
    python -m pip install xformers==0.0.19
    ```

5. **Проверка установки CUDA**:
   
    После установки библиотек torch проверьте, что CUDA установлена правильно. Откройте ваш Python и запустите следующий скрипт:
    ```
    python
    ```

    ```
    import torch

    if torch.cuda.is_available():
        print("CUDA доступна")
    else:
        print("CUDA не доступна")
    ```

    Вы должны увидеть

 сообщение "CUDA доступна", если все настроено правильно.

6. **Перейдите в папку portable**:

    ```
    cd portable
    ```

7. **Режим разработки**:
   
    Чтобы запустить в режиме разработки, используйте команду:

    ```
    briefcase dev
    ```

8. **Сборка приложения**:

    - Для сборки:

        ```
        briefcase build
        ```
    Обратите внимание, что на Windows могут возникнуть следующие ошибки после сборки: 

     ```
     'NoneType' object has no attribute 'flush'
     ```
     Для ее исправление необходимо в `wunjo/app/src/app_packages/transformers/utils/logging.py` удалить строчку `_default_handler.flush = sys.stderr.flush`.
    
     Torch после briefcase build поставился только для CPU. Необходимо скопировать из `venv\\Lib\\site-packages` torch, torch_optimizer, torchvision и заменить torch и torchvision в `wunjo/app/src/app_packages/`


    После сборки, вы найдете собранный билд в директории `portable/build`. Сборка может запускаться из `.exe` как обычная программа или из консоли. Для запуска из консоли:

        ```
        briefcase run
        ```

    Обратите внимание, при создании инсталлятора через `briefcase package` вы можете столкнуться с проблемами из-за ограничения в 2 Гб (библиотеки для GPU будут занимать место больше 2Гб) для MSI-инсталляторов на Windows. Поэтому официально распространяется только версия CPU для Windows. Вам будет достаточно сделать `briefcase build` без `briefcase package`. 

Если у вас не получается собрать приложение для GPU, посмотрите на решение частых проблем [Issue 28](https://github.com/wladradchenko/wunjo.wladradchenko.ru/issues/28).

#### Ubuntu/Debian

Приложение Ubuntu изначально совместимо с библиотеками GPU. Откройте приложение, активируйте переключатель GPU ![Скриншот с 2023-09-07 09-55-54](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/3799f33e-f333-4340-8b78-6c73dd3a290c) и вы увидите сообщение, указывающее на активацию GPU.

![Скриншот с 2023-09-07 09-56-03](https://github.com/wladradchenko/wunjo.wladradchenko.ru/assets/56233697/9b1403fd-c496-4ba9-aec2-03f35a6982a0)

#### macOS

Из-за отсутствия поддержки драйверов на macOS, к сожалению вы можете использовать приложение только на CPU. Тем не менее, вы можете модифицировать приложение для использования с альтернативами OpenCL.