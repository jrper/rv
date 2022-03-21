# Cross platform colaboration

[jrper.github.io/rv/cross_colab.html](http://jrper.github.io/rv/cross_colab.html)

j.percival@imperial.ac.uk


## Cross Platform colaboration

- Cross platform colaboration is surprising annoying.
- You may already have a little experience from Advanced Programming/Parallel Programming.
- Remember that everyone is still learning.


## Tips & Guidelines

Colaboration strategies:

- Option 1: deally want everyone using the same code base natively:
  - Plan structure before coding.
  - (eg.) CMake build system.
  - Tests & examples.
  - Single C++ standard.


- Option 2: two build systems:
  - e.g. VS code solution + Makefile
  - Less effort to start, more effort to integrate.
  - On this route, want work teams on similar machines.


- Option 3: emulation:
  - WSL lets Windows users pretend they're on *nix
  - Virtualization (e.g. UTM/parallels) can let Macs run Windows (painfully at the moment.)


General tips:
- Remember to add more tests/examples as you go
- Keep it simple.
- If in doubt, stick to standard C++.
- User interface is often biggest point of conflict.



## CMake

- Works on Windows/Mac/linux
   - on mac `brew install cmake` to install
- Works with VS code/Visual studio/command line
  - On Visual Studio open _folder_ to detect `CMakeLists.txt`


- On command line (linux/mac):
    ```
    cmake .
    make # makes everything
    ```
- On command line (Windows):
    ```
    cmake .
    msbuild Genetic_Algorithm.sln # makes everything
    ```


