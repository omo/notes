
# I want a better NDK build system.

What we have now:

 * Android.mk: Use GNU Make. Just creates .so.
   * Cons: No Java support.
   * Cons: No cross-platform support.
 * Gradle: Creates a wrapper for Android.mk
   * Pros: Great Java support (it's *the* Android build system after all.)
   * Cons: Poor C++ handling. code layout, etc.
   * Cons: No cross-platform support.
 * GYP (+ Ninja): he chromium build system including Android build
   * Pros: Natively cross-platform ... excluding Android (if you use Ninja.)
   * Cons: Android support is built on top of hooks using tons of python scripts.
   * Pros: Supports Java somehow
   * Cons: Java build is done
 * CMake-Android:
   * Pros: Cross-platform
   * Cons: No Java Support

What I want to build:

 * A C++ library with Java API for Android.
   * For non-Android, it is just a C++ library
   * For Android, it's a JAR file.
 * The native part is mostly portable, and tests for portable part can be run on the host instead of the device.
 * Sample/Demo apps as a part of the project (written in pure Java).

What I don't want:

 * A fully native application written entirely C++.
 * A Java app that has some native part. I'm fine to have native part in a library.

Options:

 * Have three build files: For Java, Native and the host.
   * That means we'll have a gradle file, an Android.mk, and whatever.
