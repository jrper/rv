# testing for C++

j.percival@imperial.ac.uk



### Stages of python testing

 1. Write tests
 2. Run tests
 3. Observe results


### Stages of C++ testing

 1. Write tests
 2. Compile tests
 3. Run tests
 4. Observe results



### C++ Testing frameworks

 - `gtest` from google
 - `cppunit`
 - *lots* of handbuilt frameworks


### C++ Testing frameworks

Similar structues in multiple frameworks:
 - `test cases` make logical assertions to test code
 - `test suites` collect cases to build executables
 - `test runners` call executables & collate results



### Genetic Algorithm project

Base project repository contains a python-based test runner `run_tests.py`,
with a Visual Studio solution file & a Makefile (for CX1/travis).

```
msbuild /p:Configuration=Test
```
or
```
make runtest
```


### Genetic Algorithm project

`run_tests.py` calls executables in `tests/bin` directory, built from `.cpp` files in
`tests`.

If an executable:
 - fails to run
 - has `fail` in its output
 test is logged as failing.


### An example test case

```
    int valid[3] = {0, 1, 2};

    if (Check_Validity(valid))
		printf("pass\n");
	else
		printf("fail\n");
```


### Another example test case

```
	int invalid[3] = {0, 2, 2};

	if (Check_Validity(invalid))
		printf("fail\n");
	else
		printf("pass\n");

```

