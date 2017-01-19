# stan-dev

The goal of this repo is to provide a CMake-based build of all Stan
components and their dependencies.  The advantages of this approach are:

- The individual repos can rely on CMake's find_library and rely on
  another project to have all the voodoo required to build dependencies
  from source.
- The version requirements are available in simple text for for editing.
  The goal is to have these in a single top-level file although
  currently it's split between the main CMakeLists.txt and the external
  project CMakeLists.txt files.
- Out-of-tree builds for all the components. Rely on CMake internal
  scripts as needed for each sub-project.


Quickstart
==========

1. Clone the repo:

```
cd ${DEV_DIR}
git clone https://github.com/sakrejda/stan-dev.git
cd stan-dev
```

2. Set option to build protostan and any missing dependencies.
   By default this includes all the required dependencies.

```
...... HOW?
```

3. Set up a build environment and build.

```
cd ${BUILD_DIR}
cmake ${DEV_DIR}/stan-dev 
make
```


4. Run tests
```
cd ${BUILD_DIR}
ctest
```
 
5. Installation, currently none.



