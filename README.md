# Andy's Git Bisect Tutorial

```sh
@macbook (master) ~/bisect-tutorial
> git bisect bad
You need to start by "git bisect start"
Do you want me to do it for you [Y/n]? y
@macbook (bisect/bad~6) ~/bisect-tutorial
> git checkout 392ec397f
Previous HEAD position was 01260e6bf Added error message
HEAD is now at 392ec397f Add new CMake build
@macbook (bisect/bad~5) ~/bisect-tutorial
> cd build
@macbook (bisect/bad~5) ~/bisect-tutorial/build
> make
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/andschwa/bisect-tutorial/build
Scanning dependencies of target tutorial
[ 50%] Building CXX object CMakeFiles/tutorial.dir/main.cpp.o
[100%] Linking CXX executable tutorial
[100%] Built target tutorial
@macbook (bisect/bad~5) ~/bisect-tutorial/build
> ./tutorial
Hello!
@macbook (bisect/bad~5) ~/bisect-tutorial/build
> git bisect good
You need to run this command from the toplevel of the working tree.
1 @macbook (bisect/bad~5) ~/bisect-tutorial/build
> cd ..
@macbook (bisect/bad~5) ~/bisect-tutorial
> git bisect good
Bisecting: 2 revisions left to test after this (roughly 1 step)
[df8acaa359d73738b43f5a80a16b0fe62e832792] More innocuous changes
@macbook (bisect/bad~3) ~/bisect-tutorial
> git status
HEAD detached at df8acaa35
You are currently bisecting, started from branch 'master'.

Untracked files:
	build/

nothing added to commit but untracked files present
@macbook (bisect/bad~3) ~/bisect-tutorial
> cd build
@macbook (bisect/bad~3) ~/bisect-tutorial/build
> make
Scanning dependencies of target tutorial
[ 50%] Building CXX object CMakeFiles/tutorial.dir/main.cpp.o
[100%] Linking CXX executable tutorial
[100%] Built target tutorial
@macbook (bisect/bad~3) ~/bisect-tutorial/build
> ./tutorial 
I think things are good!
1 @macbook (bisect/bad~3) ~/bisect-tutorial/build
> git bisect bad
You need to run this command from the toplevel of the working tree.
1 @macbook (bisect/bad~3) ~/bisect-tutorial/build
> cd ..
@macbook (bisect/bad~3) ~/bisect-tutorial
> git bisect bad
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[8e82b021fc05df84a1bf526bb18589b003c8fd4f] Totally didn't break the program here
@macbook (bisect/bad~1) ~/bisect-tutorial
> cd build
@macbook (bisect/bad~1) ~/bisect-tutorial/build
> make
Scanning dependencies of target tutorial
[ 50%] Building CXX object CMakeFiles/tutorial.dir/main.cpp.o
[100%] Linking CXX executable tutorial
[100%] Built target tutorial
@macbook (bisect/bad~1) ~/bisect-tutorial/build
> ./tutorial 
FUCK!
1 @macbook (bisect/bad~1) ~/bisect-tutorial/build
> cd ..
@macbook (bisect/bad~1) ~/bisect-tutorial
> git bisect bad
8e82b021fc05df84a1bf526bb18589b003c8fd4f is the first bad commit
commit 8e82b021fc05df84a1bf526bb18589b003c8fd4f
Author: Andrew Schwartzmeyer <andrew@schwartzmeyer.com>
Date:   Sat Jul 6 16:14:26 2019 -0700

    Totally didn't break the program here

:100644 100644 6c5bd5bf39b5d4acc1208f5bc2dd86f754fb978a 965fdf82a323654ff6dd1b2edd90a3912f1864ab M	main.cpp
@macbook (bisect/bad) ~/bisect-tutorial
> ls
CMakeLists.txt  README.md  build  main.cpp
@macbook (bisect/bad) ~/bisect-tutorial
> 
@Andys-MacBook-Pro.local (bisect/bad) ~/bisect-tutorial
> git bisect reset
Previous HEAD position was 8e82b021f Totally didn't break the program here
Switched to branch 'master'
@macbook (master) ~/bisect-tutorial
> 
```
