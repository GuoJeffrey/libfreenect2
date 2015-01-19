# libfreenect2

## Maintainers:

* Joshua Blake <joshblake@gmail.com>
* Florian Echtler
* Christian Kerl

## Description

Driver for Kinect for Windows v2 (K4W2) devices (release and developer preview).

Note: libfreenect2 does not do anything for either Kinect for Windows v1 or
Kinect for Xbox 360 sensors. Use libfreenect1 for those sensors.

This driver supports:

* RGB image transfer
* IR and depth image transfer

Missing features:

* Registration of RGB and depth images
* Audio transfer
* Firmware updates

Watch the OpenKinect wiki at www.openkinect.org and the mailing list at
https://groups.google.com/forum/#!forum/openkinect for the latest developments
and more information about the K4W2 USB protocol.

## Installation

This project has been forked from the original Kinect v2 device driver
published under http://github.com/ethz-asl/libfreenect2 in order to maintain
a build system port and some minor feature additions. Please not that this
fork is intended to support Debian-based Linux build systems only and will
most likely never be extended to other platforms.

Up to now, the build has been verified to work under Ubuntu trusty.

## Building from source

To build from source, this project requires the CMake build system with an
open-source macro extension called ReMake.

### Preparing the build system

If you already have installed ReMake on your build system, you may skip this
step. Otherwise, before attempting to build this project the traditional CMake
way, you must install ReMake following any of the two options described below:

* From source:
  * Clone ReMake from https://github.com/kralf/remake.git into
    `REMAKE_PROJECT_DIR`
    
  * Install the ReMake build dependencies (see
    `REMAKE_PROJECT_DIR/CMakeLists.txt` for details)
    
  * In the build directory, run

    ```
    cmake REMAKE_PROJECT_DIR
    ```
    
    to configure the build
    
  * Build and install the project using

    ```
    make package_install
    ```

    (from package on Debian-based Linux only) or
    
    ```
    make install
    ```
    
* From binary packages (Debian-based Linux only):
  * Add the ReMake PPA to your APT sources by issuing

    ```
    sudo add-apt-repository ppa:ethz-asl/build-essential
    ```

    on the command line
    
  * To re-synchronize your package index files, run 

    ```
    sudo apt-get update
    ```
    
  * Install the ReMake package through

    ```
    sudo apt-get install remake
    ```

### Installing build dependencies

The build dependencies of this project have been backported from more recent
releases of Ubuntu or their source code repositories. To install them, follow
these instructions:

* Add the backports PPA to your APT sources by issuing 

  ```
  sudo add-apt-repository ppa:ethz-asl/backports
  ```

  on the command line (see synopsis for the project's package PPA)

* To re-synchronize your package index files, run 

  ```
  sudo apt-get update
  ```

* Install all build depdencies through 

  ```
  sudo apt-get install libusb-1.0-0-dev ocl-icd-libopencl1 opencl-headers libglfw3-dev libglewmx-dev libopencv-dev libturbojpeg libjpeg-turbo8-dev libboost-program-options-dev
  ```

### Building with CMake

Once ReMake is available on your build system, you may attempt to build this
project the CMake way. Assuming that you have cloned the project sources into
`PROJECT_DIR`, a typical out-of-source build might look like this:

* Create a build directory using 

  ```
  mkdir -p PROJECT_DIR/build
  ```

* Switch into the build directoy by 

  ```
  cd PROJECT_DIR/build
  ```

* In the build directory, run 

  ```
  cmake PROJECT_DIR
  ```

  to configure the build

* If you want to inspect or modify the build configuration, issue 

  ```
  ccmake PROJECT_DIR
  ```

* Build the project using 

  ```
  make
  ```

* If you intend to install the project, call 

  ```
  make packages_install
  ```

  (from package(s) on Debian-based Linux only) or 

  ```
  make install
  ```

## Installing from packages

The maintainers of this project provide binary packages for the latest Ubuntu
LTS releases and commonly used system architectures. To install these packages,
you may follow these instructions:

* Add the backports PPA to your APT sources by issuing 

  ```
  sudo add-apt-repository ppa:ethz-asl/backports
  ```

  on the command line

* Add the project PPA to your APT sources by issuing 

  ```
  sudo add-apt-repository ppa:ethz-asl/drivers
  ```

  on the command line

* To re-synchronize your package index files, run

  ```
  sudo apt-get update
  ```

* Install all project packages (and their dependencies) through

  ```
  sudo apt-get install libfreenect2*
  ```

  or selected packages using your favorite package management tool

## Required notification

The K4W2 hardware is currently pre-release. Per the K4W2 developer program
agreement, all public demonstrations and code should display this notice:

    "This is preliminary software and/or hardware and APIs are preliminary and subject to change."
