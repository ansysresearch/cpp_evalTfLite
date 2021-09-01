# cpp_evalTfLite
A repo using lightweight tensorflowLite cpu Library for deployment

This repo provides a pure lightweight C++ based CPU library for deployment of Tensorflow trained ML models based on TensorflowLite as well as provides an example executable how to use the tensorflowLite lib. The code can build for both Linux/Windows using cmake tools. Details on how to build is provided as well. 

Assumptions:
Tensorflow ML model is trained before archived in /Model folder. There is a relative reference to this folder in client executable.

Compatibility: All versions tensorflow and C++ 15 and above.

How to build?

For Building on windows or Linux just use the top level cmake file which first builds the tensorflowLite library and shows how to use it in the exe.
If Cmake is not installed, install it for Windows or Linux first below Step 1.  

Step 1: Install Cmake(3.16 or higher): For Linux/Ubuntu, you can simply run the following command: 
sudo apt-get install cmake

For windows: Download Cmake(3.16 or higher) from https://cmake.org/download/
Extract the zip and install.

Step 2: Clone this repo. It will create cpp_evalTfLite folder. CD to this folder.

Step 3: Clone TensorFlow repository inside cpp_evalTfLite: git clone https://github.com/tensorflow/tensorflow.git tensorflow_src

Step 4: Create CMake build directory and change to this directory, On Linux:
mkdir tflite_build
cd tflite_build

Step 5: Run CMake tool with configurations, It generates an optimized release binary by default. If you want to build for your workstation, simply run the following command:
cmake ../tensorflow_src/tensorflow/lite or cmake ../tensorflow_src/tensorflow/lite -DCMAKE_BUILD_TYPE=Debug 

Step 6: Build TensorFlow Lite Lib and client executable using top level cmake. Go two level up to cpp_evalTfLite folder 
In the cpp_evalTfLite directory
Linux: cmake --build . -j or cmake --build build -- -j3
Windows: cmake -H. -Bbuild

Step 7: Run the Exe 
In the cpp_evalTfLite directory
Linux: ./build/TestingTfLiteCpuDeployment
Windows: Cmake will only create the VS Project files: You will need to compile and link all binaries using VS.

Note on compile time and run time dependencies: All runtime dependencies are generated in top level build folder:

Tesorflow static Lib compile time dependencies:

tensorflow_src
tensorflow_src\tensorflow\lite\schema
build\pthreadpool-source\include
build\xnnpack\include
build\cpuinfo-source
build\eigen
build\neon2sse
build\abseil-cpp
build\farmhash\src
build\flatbuffers\include
build\gemmlowp\public
build\gemmlowp
build\ruy
build\FP16-source\include


Client Application dependencies runtime:
tensorflow-lite\Release\tensorflow-lite.lib
cpuinfo\Release\cpuinfo.lib
clog\Release\clog.lib
pthreadpool\Release\pthreadpool.lib
+All in build\_dep folder as below, Search for *.lib extension
