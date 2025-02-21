# PyTorch 2.6.0 (Без AVX) для Windows

Этот релиз представляет собой сборку **PyTorch 2.6.0**, **без поддержки AVX**, для процессоров, не имеющих инструкций AVX/AVX2/AVX512.

<table>
  <tr><td>✅ <b>Версия:</b> <code>2.6.0a0+git1eba9b3</code></td></tr>
  <tr><td>✅ <b>Python:</b> <code>3.10</code></td></tr>
  <tr><td>✅ <b>Операционная система:</b> <code>Windows 64-bit (win_amd64)</code></td></tr>
  <tr><td>✅ <b>CPU:</b> <code>SSE2 (без AVX, AVX2, AVX512)</code></td></tr>
  <tr><td>✅ <b>CUDA:</b> 🟥 Нет</td></tr>
  <tr><td>✅ <b>OpenMP:</b> ✅ Включен</td></tr>
  <tr><td>✅ <b>MKLDNN:</b> ✅ Включен</td></tr>
  <tr><td>✅ <b>Компилятор:</b> <code>MSVC 19.43.34808.0</code></td></tr>
  <tr><td>✅ <b>C++ Стандарт:</b> <code>C++17</code></td></tr>
</table>

### 🔧 Полная информация о сборке:

PyTorch built with:

- C++ Version: 201703
- MSVC 194334808
- Intel(R) MKL-DNN v3.5.3 (Git Hash 66f0cb9eb66affd2da3bf5f8d897376f04aae6af)
- OpenMP 2019
- CPU capability usage: NO AVX

Build settings:

- BUILD_TYPE=Release
- CXX_COMPILER=MSVC 19.43.34808
- CXX_FLAGS=/arch:SSE2 /utf-8 -DUSE_PTHREADPOOL -DUSE_KINETO -DLIBKINETO_NOCUPTI
- USE_CUDA=OFF, USE_MKL=OFF, USE_MKLDNN=ON, USE_OPENMP=ON

🚀 Установка:

Установите его в ваше виртуальное окружение указав путь до файла:

`pip install C:\torch-2.6.0a0+git1eba9b3-cp310-cp310-win_amd64.whl`

📌 Проверка работы:

Создайте файл `main.py` и вставьте код:

```python
import torch

print("Версия PyTorch:", torch.__version__)
print("Полная информация о сборке:")
print(torch.__config__.show())
```

Запустите: `python main.py`

🛠 Кому подойдет эта сборка?

Вы используете Python 3.10.
У вас старый процессор, не поддерживающий AVX.
Вам нужен PyTorch 2.6.0 на Windows 64-bit.

# Руководство по сборке PyTorch 2.6.0 без AVX для Windows

Это руководство описывает, как собрать PyTorch 2.6.0 без поддержки AVX (для процессоров, не имеющих инструкции AVX/AVX2/AVX512) с использованием Python 3.10.

> **Важно:** При сборке в Windows используйте пути, содержащие только латинские символы.

---

###### Для выхода из виртуальной среды используйте эту команду: `deactivate`

###### Если вам нужно чтобы PyTorch работал с другой версией Python, используйте свою версию за место указанной ниже Python 3.10

###### В VScode я использую терминал bash, по этому все команды основаны на нём.

---

### Требования

**requirements.txt** – зависимости для сборки PyTorch:
`numpy ninja pyyaml mkl mkl-include typing_extensions packaging requests tqdm sympy filelock`

### Подготовка окружения (для VSCode с терминалом bash)

**1. Склонируйте данный репозиторий в папку с именем, содержащим только латинские буквы.** Например, в корневой каталог проекта:

```sh
   git clone https://github.com/brend8c/PyTorch-2.6.0-without-AVX.git
```

**2. Выберите нужную версию Python для интерпретатора:**  
В VSCode нажмите `Ctrl+Shift+P` и пишем `Python: Select Interpreter`. Выберите Python 3.10.

**3. Создайте виртуальное окружение:**  
"C:\Python310\python.exe" -m venv myenv

**4. Активируйте виртуальное окружение:**  
source myenv/Scripts/activate

**5. Укажите интерпретатор Python в VSCode:**  
Нажмите `Ctrl+Shift+P` и пишем `Python: Select Interpreter`, затем выберите `.\myenv\Scripts\Python.exe`

**6. Обновите pip и установите зависимости:**  
`python -m pip install --upgrade pip`  
`pip install -r requirements.txt`  
`pip install cmake setuptools wheel`

**7. Клонируйте в корневой каталог проекта:**  
PyTorch-2.6.0-without-AVX\ `git clone --recursive --branch v2.6.0 https://github.com/pytorch/pytorch.git`

### Установка системных зависимостей:

**1. Скачайте Visual Studio 2022 Build Tools:**  
[Visual Studio 2022 Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

**2. Установите необходимые компоненты:**  
Импортируйте настройки из файла `.vsconfig` или установите вручную требуемые компоненты.

**3. Отключите AVX в CMake:**  
Откройте файл `PyTorch-2.6.0-without-AVX\pytorch\CMakeLists.txt`

Найдите следующий фрагмент кода:

```
# ---[ Project and semantic versioning.
project(Torch CXX C)
```

и сразу после него добавьте:

```
if(MSVC)
    # Удаляем флаг AVX (если присутствует) и принудительно устанавливаем SSE2
    string(REPLACE "/arch:AVX" "" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /arch:SSE2")
endif()
```

**1. В Windows в строке поиска введите и откройте**  
`x64 Native Tools Command Prompt for VS 2022`  
Это командная строка, в которой настроена среда компиляции (VC++).

**2. Перейдите в каталог с проектом:**  
`cd /d E:\PyTorch-2.6.0-without-AVX`

**3. Активируйте ваше виртуальное окружение Python 3.10:**  
**Введите команду из корневого каталога проекта (где находится папка myenv):**  
E:\PyTorch-2.6.0-without-AVX> `myenv\Scripts\activate`

**4. Перейдите в каталог с исходным кодом PyTorch (там, где находится `setup.py`):**  
`cd pytorch`

**5. Установите переменные окружения для сборки без AVX и корректного пути HOME:**  
`set HOME=C:\Users\brend`
`set USE_AVX=0`

**6. Запустите сборку PyTorch:**  
`python setup.py install`

- Обратите внимание, что компиляция может занять около 3 часов при полной загрузке CPU.
- Если всё прошло успешно и нет логов об ошибках, можем собрать wheel‑файл.
- Wheel — это стандартный бинарный дистрибутив для Python, который содержит скомпилированный код и метаданные. Он предназначен для быстрой и удобной установки пакетов через pip.

– После сборки в каталоге `PyTorch-2.6.0-without-AVX\` и `PyTorch-2.6.0-without-AVX\pytorch\` появится папка `build`.
– Если что-то пошло не так и во время сборки вы получили ошибку, после устранения ошибки удалите папку `build` в `PyTorch-2.6.0-without-AVX\pytorch\build` и повторите попытку сборки.

**7. Сборка wheel‑файла:** вводим и запускаем команду:  
(myenv) E:\PyTorch-2.6.0-without-AVX\pytorch> `python setup.py bdist_wheel`

- После успешной сборки wheel‑файл появится в каталоге `PyTorch-2.6.0-without-AVX\pytorch\dist` (например, что-то вроде torch-2.6.0a0+git1eba9b3-cp310-cp310-win_amd64.whl).

---

# Использование собранного PyTorch

**1. Установка в другое виртуальное окружение:**
`pip install путь/до/torch-2.6.0a0+git1eba9b3-cp310-cp310-win_amd64.whl`

**2. Проверка установки:**
Создайте файл `main.py` со следующим кодом:

```python
import torch
print("Версия PyTorch:", torch.__version__)
print("Полная информация о сборке:")
print(torch.__config__.show())
```

Запустите: `python main.py`

**В выводе должно быть указано:**
`CPU capability usage: NO AVX`
что подтверждает сборку без поддержки AVX.

**Отменяем временные переменные:**  
Достаточно удалить их из текущей сессии. Если вы работаете в Git Bash, выполните следующие команды:
`unset HOME`
`unset USE_AVX`
