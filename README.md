Travis-CI: [![Build Status](https://travis-ci.com/nasa/cFS.svg)](https://travis-ci.com/nasa/cFS)

# Core Flight System - Gateway BUNDLE of open source apps

This repository is a bundle of submodules that make up the Core Flight System (cFS) framework plus the open source GSFC apps included for Gateway.

Note the "lab" apps are include for open source test capability, and enable this bundle to build, execute, receive commands, and send telemetry.  This is not a flight distribution, which is typically made up of the cFE, OSAL, PSP, and a selection of flight apps that coorespond to specific mission requirements.

## Version Notes
  - This is simply for tracking versions and configuration for Gateway

## Known issues
  - See submodules

## Major future work
  - No major development planned in this branch

## Setup

To setup the cFS BUNDLE directly from the latest set of interoperable repositories:

    git clone --branch dev-gw https://github.com/nasa/cFS.git
    cd cFS
    git submodule init
    git submodule update

Unique to this branch - sample_defs provided by this branch

    cp cfe/cmake/Makefile.sample Makefile

If running on a standard linux build as a normal user, define OSAL_DEBUG_PERMISSIVE_MODE for best effort message queue depth and task priorities.

    sed -i 's/undef OSAL_DEBUG_PERMISSIVE_MODE/define OSAL_DEBUG_PERMISSIVE_MODE/g' sample_defs/default_osconfig.h

## Build and Run

This bundle will build and run on the pc-linux platform support package (should run on most Linux distributions), via the steps described in https://github.com/nasa/cFE/tree/master/cmake/README.md.  Quick-start is below:

To prep, compile, and run on linux host (from cFS directory above):

    make SIMULATION=native prep
    make
    make install
    cd build/exe/cpu1/
    ./core-cpu1

Should see startup messages, and CFE_ES_Main entering OPERATIONAL state.  Note the code must be executed from the build/exe/cpu1 directory to find the startup script and shared objects.

## Send commands, receive telemetry

The cFS-GroundSystem tool can be used to send commands and receive telemetry (see https://github.com/nasa/cFS-GroundSystem/tree/master/Guide-GroundSystem.txt, the Guide-GroundSystem.txt).  Note it depends on PyQt4 and PyZMQ:

1. Install PyQt4 and PyZMQ on your system
2. Compile cmdUtil and start the ground system executable

       cd tools/cFS-GroundSystem/Subsystems/cmdUtil
       make
       cd ../..
       python GroundSystem.py
    
3. Select "Start Command System"
4. Select "Enable Tlm"
5. Enter IP address of system executing cFS, 127.0.0.1 if running locally

Should see telemetry, can send noops and see command counters increment
