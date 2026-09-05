# Coral Dev Board Micro source code (coralmicro)

This repository contains all the code required to build apps for the [Coral Dev
Board Micro](https://coral.ai/products/dev-board-micro). The Dev Board Micro is
based on the NXP RT1176 microcontroller (dual-core MCU with Cortex M7 and M4)
and includes an on-board camera (324x324 px), a microphone, and a Coral Edge TPU
to accelerate TensorFlow Lite models.

The software platform for Dev Board Micro is called `coralmicro` and is based
on [FreeRTOS](https://www.freertos.org/). It also includes libraries for
compatibility with the Arduino programming language.

The `coralmicro` build system is based on CMake and includes support for Make
and Ninja builds. After you build the included projects, you can flash
them to your board with the included flashtool (`scripts/flashtool.py`).

This course fork also provides a local keyword-spotting training notebook and
supporting Python files for MF2143 Tutorial 2.

![main](https://github.com/google-coral/coralmicro/actions/workflows/ci.yml/badge.svg?event=push)
![arduino](https://github.com/google-coral/coralmicro/actions/workflows/arduino.yml/badge.svg?event=push)


## Documentation

+ [Get Started with the Dev Board Micro](https://coral.ai/docs/dev-board-micro/get-started/)

+ [Get Started with Arduino](https://coral.ai/docs/dev-board-micro/arduino/)

+ [Build an out-of-tree project](https://github.com/google-coral/coralmicro-out-of-tree-sample/blob/main/README.md)

+ [coralmicro API reference](http://coral.ai/docs/reference/micro/)

+ [coralmicro examples](/examples/)


## Get the code

If the Coral Micro SDK was installed during an earlier tutorial, do not clone
another copy. Verify the existing checkout with:

```bash
cd <ROOT>/coral_dev_board/coralmicro
git remote -v
git status
git submodule status
```

Here, `<ROOT>` is a placeholder for the local course root and must be replaced
with the actual path.

For a new installation, clone this course fork and all submodules:

```bash
git clone --recurse-submodules -j8 https://github.com/djchende9/coralmicro.git
```

Install the required Coral Micro SDK tools:

```bash
cd coralmicro && bash setup.sh
```


## Tutorial 2 keyword-training files

The course-specific training resources are:

+ [Keyword Spotting Model Training](train_keyword_complete.ipynb)
+ [TFLite conversion script](convert_to_tflite.py)
+ [Python requirements](requirements.txt)

The notebook uses Python 3.11 and TensorFlow 2.20.0. For the course workflow,
copy these files into the Tutorial 2 model-training workspace rather than
creating another complete Coral SDK checkout.


## Build the code

This builds everything in a folder called `build` (or you can specify a
different path with `-b`, but if you do then you must specify that path
every time you call `flashtool.py`):

```bash
bash build.sh
```

## Flash the board

This example blinks the board's green LED:

```bash
python3 scripts/flashtool.py -e blink_led
```

You can see the code at [examples/blink_led/](examples/blink_led/).


### Reset the board to Serial Downloader

Flashing the Dev Board Micro might fail sometimes and you can usually solve
it by starting Serial Downloader mode in one of two ways:

+ Hold the User button while you press the Reset button.
+ Or, hold the User button while you plug in the USB cable.

Then try flashing the board again.

For more details, see the [troubleshooting info on
coral.ai](https://coral.ai/docs/dev-board-micro/get-started/#serial-downloader).


## Update the repo

Use the following commands to keep all coralmicro submodules in sync (rebasing
your current branch):

```bash
git fetch origin
git rebase origin/main
git submodule update --init --recursive
```
