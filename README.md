# kotlin-native-performance-experiment

This repo, reproduces the [KorGE bunnymark-fast](https://github.com/korlibs/korge-next/blob/046c9b407f4b8e134d266bd7fcf0773a0a020c4f/samples/bunnymark-fast/src/commonMain/kotlin/main.kt) update code that is slow on Kotlin/Native, it is self-contained, except when marking all the methods as inline (that hurts performance on JVM and JS).

There are three self-contained implementations without external dependencies adjusting inlining `const val` and marking all the methods as `inline`:

* Inlined: <https://github.com/korlibs/kotlin-native-performance-experiment/blob/master/src/nativeMain/kotlin/inlined/code.kt>
* Non-Inlined, but const val is not used: <https://github.com/korlibs/kotlin-native-performance-experiment/blob/master/src/nativeMain/kotlin/noninlinedbutconst/code.kt>
* Non-Inlined anything and const val is used: <https://github.com/korlibs/kotlin-native-performance-experiment/blob/master/src/nativeMain/kotlin/noninlined/code.kt>

## Kotlin 1.5.0 (Windows)

```
> Task :runReleaseExecutableNative
Executing INLINED...
Executed INLINED sixty frames in 703ms
Executing NON-INLINED-BUT-CONST...
Executed NON-INLINED-BUT-CONST sixty frames in 1.03s
Executing NON-INLINED...
Executed NON-INLINED sixty frames in 26.5s
```

## Kotlin 1.5.0 (Linux)

<https://github.com/korlibs/kotlin-native-performance-experiment/runs/2478341432?check_suite_focus=true#step:5:64>

```
Executing INLINED...
Executed INLINED sixty frames in 1.04s
Executing NON-INLINED-BUT-CONST...
Executed NON-INLINED-BUT-CONST sixty frames in 1.71s
Executing NON-INLINED...
Executed NON-INLINED sixty frames in 4.84s
```

## Kotlin 1.4.32 (Windows)

```
Executing INLINED...
Executed INLINED sixty frames in 865ms
Executing NON-INLINED-BUT-CONST...
Executed NON-INLINED-BUT-CONST sixty frames in 38.7s
Executing NON-INLINED...
Executed NON-INLINED sixty frames in 63.3s
```

## Kotlin 1.4.32 (Linux)

<https://github.com/korlibs/kotlin-native-performance-experiment/runs/2478337835?check_suite_focus=true#step:5:84>

```
Executing INLINED...
Executed INLINED sixty frames in 1.26s
Executing NON-INLINED-BUT-CONST...
Executed NON-INLINED-BUT-CONST sixty frames in 6.02s
Executing NON-INLINED...
Executed NON-INLINED sixty frames in 9.17s
```
