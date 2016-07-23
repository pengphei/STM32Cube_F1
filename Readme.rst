=======================================
STM32Cub for STM32F10X
=======================================

STM32Cub for STM32F10X series chips, based on scons.


Build
=======================================

we can build specified project in Projects folder:

.. code-block:: sh

   scons project=DEMO-C8T6

if we just using scons without specifying project, it will try to build
the default project specified in SConstruct building script.
