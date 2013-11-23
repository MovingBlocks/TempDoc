## This page is under contruction and not yet final!

### General style 
* use // TODO comments to note where something needs to be done
* Don't use Hungarian notation to denote types
* Where there are underscores before variables - feel free to remove them
* No mass imports such as import java.util.* except for static imports
* Default line width: 120 chars

### Coding-related
* Use interfaces over concrete classes for variables (e.g. Map instead of HashMap). 
* Feel free to use guava to construct the actual instance (e.g. Maps.newHashMap())

### Other
Most settings can be applied automatically through the IDE. See [[Alternative Setups]] or, more specifically [[Checkstyle]] on how to setup Checkstyle.

## Example java snippet
```java
/*
 * Copyright 2013 MovingBlocks
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package mypackage;

import java.util.List;

/**
 * An example for comment formatting.
 * @author John Doe
 */
abstract class Test {
    // This is a long comment with whitespace that should be split in multiple
    // line comments in case the line comment formatting is enabled
    abstract int foo3();

    /* block comment on first column */
    private static final int[] myArray = { 1, 2, 3, 4, 5, 6 };

    /**
     * Source formatting within javadoc comments:
     * 
     * <pre>
     * final int a = 1;
     * </pre>
     * 
     * @param a The first parameter. 0 and 100.
     * @param b The second parameter.
     * @return The result
     */
    int bar3(int a, int b) {
	do {
	    bar3();
	} while (true);

	try {
	    foo();
	} catch (Exception e) {
	    e.printStackTrace();
	} finally {
	    // ignore
	}

	return 42;
    }
}

@interface MyAnnotation {
    int count() default 1;
}
```