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

project = ARGUMENTS.get('project','DEMO-RET6')

EXE_PATH = '/home/kurain/build/gcc-arm-none/bin'
PREFIX = EXE_PATH+ '/arm-none-eabi-'

genv = Environment()

# toolchains variables
genv["CC"] = PREFIX + 'gcc'
genv["AS"] = PREFIX + 'as'
genv["AR"] = PREFIX + 'ar'
genv["LINK"] = PREFIX + 'gcc -v'
genv["OBJCOPY"] = PREFIX + 'objcopy'
genv["NM"] = PREFIX + 'nm'
genv.PrependENVPath ('PATH', EXE_PATH)

# applicationi variable
genv["PROJECT"] = project
genv["PROJECT_ROOT"] = "#Projects/" + project
genv["PROJECT_OUT"] = "#build/out"
genv["PROJECTS"] = os.listdir("Projects")

genv["STM32_DRIVERS_PATH"] = "#Drivers"
genv["STM32_MIDDLEWARES_PATH"] = "#Middlewares"
genv["STM32_FREERTOS_PATH"] = "#Middlewares/Third_Party/FreeRTOS"

Export("genv")

script = 'SConscript'
genv.SConscript(script, variant_dir="build")
