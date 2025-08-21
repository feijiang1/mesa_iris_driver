NVK
===

NVK is a Vulkan driver for NVIDIA GPUs.

Hardware support
----------------

NVK currently supports Maxwell (some GTX 700 and 800 series, most 900
series) and later GPUs up to and including Ada (RTX 4000 series).  Support
for Kepler (GeForce 600 and 700 series) and Blackwell (RTX 5000 series) is
currently in-progress but incomplete.

Conformance status:
-------------------

NVK is a conformant Vulkan 1.4 implementation for all officially supported
GPUs.

OpenGL support through Zink:
----------------------------

Starting with Mesa 25.1, all Turing (RTX 2000 series and GTX 16xx) and
later GPUs will get NVK+Zink as their OpenGL implementation by default
instead of the old Nouveau GL driver.  NVK+Zink is a conformant OpenGL 4.6
implementation.

Kernel requirements
-------------------

NVK requires at least a Linux 6.6 kernel

Debugging
---------

Here are a few environment variable debug environment variables
specific to NVK:

.. envvar:: NAK_DEBUG

   a comma-separated list of named flags affecting the NVK back-end shader
   compiler:

   ``print``
      Prints the shader at various stages of the compile pipeline
   ``serial``
      Forces serial instruction execution; this is often useful for
      debugging or working around dependency bugs
   ``spill``
      Forces the GPR file to a minimal size to test the spilling code
   ``annotate``
      Adds extra annotation instructions to the IR to track information
      from various compile passes

.. envvar:: NVK_DEBUG

   a comma-separated list of named flags, which do various things:

   ``push``
      Dumps all pushbufs to stderr on submit.  This requires that
      ``push_sync`` also be set.
   ``push_sync``
      Waits for submit to complete before continuing
   ``zero_memory``
      Zeros all VkDeviceMemory objects upon creation
   ``vm``
      Logs VM binds and unbinds
   ``no_cbuf``
      Disables automatic promotion of UBOs to constant buffers

.. envvar:: NVK_I_WANT_A_BROKEN_VULKAN_DRIVER

   If defined to ``1`` or ``true``, this will enable enumeration of all
   GPUs Kepler and later, including GPUs for which hardware support is
   poorly tested or completely broken.  This is intended for developer use
   only.

Hardware Documentation
----------------------

What little documentation we have can be found in the `NVIDIA open-gpu-doc
repository <https://github.com/NVIDIA/open-gpu-doc>`__.  The majority of
our documentation comes in the form of class headers which describe the
class state registers.
