#
# Copyright (C) 2015 Focalcrest, Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

import os

Import('genv')

# stm32 building flags
genv["STM32_CFLAGS"] = [
    '-mthumb', '-fno-builtin', '-mcpu=cortex-m3',
    '-Wall', '-std=gnu99', '-ffunction-sections', '-fdata-sections',
    '-fomit-frame-pointer', '-fno-unroll-loops', '-ffast-math',
    '-ftree-vectorize'
]
genv["STM32_CXXFLAGS"] = [
    '-mthumb', '-fno-builtin', '-mcpu=cortex-m3',
    '-Wall', '-std=c++11', '-ffunction-sections', '-fdata-sections',
    '-fomit-frame-pointer', '-fno-unroll-loops', '-ffast-math',
    '-ftree-vectorize'
]

genv["STM32_ASFLAGS"] = [
    '-mthumb', '-mcpu=cortex-m3'
]

genv["STM32_LDFLAGS"] = [
    '--static', 
]

# custom building configuration
genv["CFLAGS"] += genv["STM32_CFLAGS"]
genv["LINKFLAGS"] += genv["STM32_LDFLAGS"]
genv["ASFLAGS"] += genv["STM32_ASFLAGS"]

if genv["PROJECT"] in genv["PROJECTS"]:
    app_script = "Projects/" + genv["PROJECT"] + "/SConscript"
    app_files = SConscript(app_script)
    genv.Install(genv["PROJECT_OUT"], app_files)


