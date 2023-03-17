# How To Build Tensorflow From Source

## Why you should build tensorflow from source?
If you want to run tensorflow on old machine. and getting warnings or AVX or sse instructions error you should build tensorflow from source code
## Prerequisites
1. Install basic dependencies
    - `sudo apt install python3-dev python3-pip`
2. Installing Bazel on Ubuntu

    -  ` sudo apt install apt-transport-https curl gnupg -y`

    -  ` curl -fsSL https://bazel.build/bazel-release.pub.gpg | gpg --dearmor >bazel-archive-keyring.gpg`

    - ` sudo mv bazel-archive-keyring.gpg /usr/share/keyrings`

    - `echo "deb [arch=amd64 signed-by=/usr/share/keyrings/bazel-archive-keyring.gpg] https://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list `

    - ` sudo apt update && sudo apt install bazel `

## Steps to build

1. Clone source and create brach from version tag
    - ` git clone https://github.com/tensorflow/tensorflow.git`
    - `cd tensorflow `
    - `git checkout -b newbranch v2.11.0`
2. Build using Bazel. Update ram/cpu& jobs as per system config - it can take updato 10 hours
    - ` - bazel build --config=opt --local_ram_resources=2048 --local_cpu_resources=HOST_CPUS-1 --jobs=1
  //tensorflow/tools/pip_package:build_pip_package`
3. Compiled TensorFlow into a Python Wheel package
    - `./bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg`
4. Install via pip
    - ` cd /tmp/tensorflow_pkg`
    - ` pip instal tensorflow-2.2.0-cp36-cp36m-linux_x86_64.whl`


Ref:
- https://bazel.build/install/ubuntu
- https://www.tensorflow.org/install/source
- https://gsverhoeven.github.io/post/deep-learning-tensorflow-keras/
