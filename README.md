Description

A high-performance, on-device AR kernel targeting Ray-Ban Meta powered by Snapdragon AR1. Implements stereo-vision SLAM, a 478-node FaceMesh model via TensorFlow Lite (flatbuffers), procedural frame overlays with GLSL, and low-level power-governor hooks to meet the following targets:

Latency: ≤ 60 ms (formula 1)

Power Draw: ≤ 2.9 W

Stability: ≥ 99 % crash-free sessions

Requirements

Platform: Snapdragon AR1, Android 13 AOSP

Engine: Unity LTS 2024.2, OpenXR 1.1

Languages: C++17 (native), C# (Unity), GLSL

Models: TensorFlow Lite flatbuffers (.tflite)
ARKernelProject/
├── README.md
├── native/
│   ├── CMakeLists.txt
│   ├── include/
│   │   ├── StereoSLAM.h
│   │   ├── FaceMeshModel.h
│   │   └── PowerGovernor.h
│   └── src/
│       ├── StereoSLAM.cpp
│       ├── FaceMeshModel.cpp
│       └── PowerGovernor.cpp
├── unity/
│   └── Assets/
│       ├── Scripts/
│       │   └── ARKernelManager.cs
│       └── Plugins/
│           └── libarkernel.so (built from native)
├── shaders/
│   ├── frame_overlay.vert
│   └── frame_overlay.frag
└── models/
    └── FaceMesh_478.tflite

    # On-Device AR Kernel (Ray-Ban Meta)

## Overview
This package provides an on-device AR kernel tailored for Ray-Ban Meta glasses. It fuses stereo-vision SLAM with a FaceMesh inference pipeline, applying real-time overlays via GLSL shaders and managing power states via kernel hooks.

## Setup & Build

1. **Clone Repository**
   ```bash
   git clone https://github.com/yourorg/ARKernelProject.git
   cd ARKernelProject

   mkdir -p native/build && cd native/build
cmake .. -DCMAKE_TOOLCHAIN_FILE=$ANDROID_NDK/build/cmake/android.toolchain.cmake \
      -DANDROID_ABI=arm64-v8a -DANDROID_PLATFORM=android-33
make -j8

