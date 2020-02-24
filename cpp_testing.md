# SPH Code & Testing for C++

[jrper.github.io/rv/cpp_testing.html](http://jrper.github.io/rv/cpp_testing.html)

j.percival@imperial.ac.uk



### SPH Repository stub

Stub follows generic template

- `.travis.tml` for Travis
- `Makefile` to build on Travis
- `README.md` for GitHub
- `requirements.txt` for useful Python modules
- `include/` for header files
- `src/` for `.cpp` files
- `tests/` for test files



### Software Sustainability in ACSE 4.3

- Core programming language now C++
- Continued expectation that code will be:
  * clear
  * correct
  * extendable
  * robust
- Testing helps to tick these boxes
  


### Three Stages of Python testing

 1. Write tests
 2. Run tests
 3. Observe results


### Four Stages of C++ testing

 1. Write tests
 2. __Compile tests__
 3. Run tests
 4. Observe results



### C++ Testing frameworks

 - [`googletest`](https://github.com/google/googletest) aka [`gtest`](https://github.com/google/googletest) from Google
 - [`boost.test`](https://www.boost.org/doc/libs/1_70_0_beta1/libs/test/doc/html/index.html) part of the BOOST libraries
 - [`cppunit`](http://cppunit.sourceforge.net/doc/1.8.0/) Veteran framework, not Windows friendly.
 - *lots* of handbuilt frameworks
 - As usual [wikipedia](https://en.wikipedia.org/wiki/List_of_unit_testing_frameworks#C++) has a table.


### C++ Testing frameworks

Similar structures in multiple frameworks:
 - _`test cases`_ make logical assertions to test code
 - _`test suites`_ collect cases to build executables
 - _`test runners`_ call executables & collate results
Often more boilerplate than `pytest`



### Smoothed Particle Hydrodynamics project

Template project repository contains a simple hand-rolled Python-based test runner `run_tests.py`,
with a Makefile (for CX1/Travis).

```
make runtests
```

Code will also compile/run on Windows with a suitable Visual Studio setup.


### Smoothed Particle Hydrodynamics project

`run_tests.py` calls executables in `tests/bin` directory, built from `.cpp` files in
`tests`.

If an executable:
 - fails to run
 - has `fail` in its output
 test is logged as failing.

Also runs Python functions in `python_tests.py` files in `tests`


### An example C++ test case

```
	// my_function test case
	std::cout << "Test my_function: ";

    int mock_input[3] = {0, 1, 2};

    if (my_function(mock_input) == 3)
		std::cout << "pass\n";
	else
		std::cout << "fail\n";
```


### An example C++ test case

Can put in the `main` of `test_SPH_2d.cpp`, or as separate function.

Can call the test executables directly to see errors

```
$ ./tests/bin/test_SPH_2D
Test my_function: pass
```


### Can also check output with Python

E.g.`file_writer.cpp` is a zero-dependency code outputting particle data in a [ParaView](https://www.paraview.org/) readable [VTK file format](https://vtk.org/wp-content/uploads/2015/04/file-formats.pdf).

`test_file_writer.cpp` just generates data and calls functions.

Check output using the Python `vtk` module.


```
import vtk

def test_file_writer_output():
    reader = vtk.vtkXMLPolyDataReader()
    reader.SetFileName('tests/test_file_writer.vtp')
    reader.Update()

    pdata = reader.GetOutput()
    assert pdata.GetPoint(5) == (5.0, 5.0, 0.0)
```



### The Makefile

Lots of things aren't currently tested.
You may want to add tests/files.

One option is to just add more test cases to existing files:

```
tests/test1.cpp
tests/test2.cpp
```

Easy to modify, but can cause conflicts on github.


### The Makefile

Another good option is to have (at least) one test file for each work package, eg:
 - Core SPH code
 - IO
 - Post-processing

Also tells you who to talk to:


### The Makefile

Add C++ test files to <akefile by copying structure from the lines for `test_file_writer`

```

TESTS = test_blah_blah

test_blah_blah: $(TEST_BIN_DIR)/test1

$(TEST_BIN_DIR)/test1: $(TEST_BUILD_DIR)/blah_blah.o \
                             $(BUILD_DIR)/other_file.o
	     $(CXX) -o $@ $^

```
