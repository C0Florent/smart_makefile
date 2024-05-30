# Smart Makefile

A "smart" build system for C/C++ built using GNU make, which rebuilds sources if headers they depend on are updated.

---

This repository contains several examples of Makefiles, all in seperate directories.


## example1

This contains a basic example where a "simple" Makefile doesn't update properly the object files when headers are changed.

## example1_auto

This is a slightly improved version of the example1 where header dependencies are manually described. This sure rebuilds when needed, but is not scalable for growing projects

## rules

A simple demonstration of how Makefile rules can call each other and how they decide if their target is up to date or not

## live_demo

The simplest version of a scalable Makefile which tracks dependencies and updates object files when needed. It was built live during a presentation, and actually only consists in the "simple" Makefile of *example1* with 4 actual code lines added
