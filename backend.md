# Back-end Code Standards

## PHP

### Inline Documentation
All docblocks must be compatible with the phpDocumentor format. For more information on that format, visit <a href="http://phpdoc.org/" title="phpdoc.org">http://phpdoc.org/</a>.

#### Functions
Every function must have a docblock that contains at a minimum the following.

```
/**
 * This is what this function does. (short description)
 *
 * @param  array    $aCategories Just a handful of categories
 * @param  integer  $sRepeat     How many times something should happen
 * @param  boolean  $sRandom     Randomize the results
 * @return array
 */
public function doSomethingInteresting($aCategories, $sRepeat = 1, $sRandom = false) {
	// implementation...
}
```

### Function Calls
Functions should be called with no spaces between the function name, the opening parenthesis, and the first parameter; spaces between commas and each parameter, and no space between the last parameter, the closing parenthesis, and the semicolon.

```
// Correct
$var = foo($bar, $baz, $quux);

// Incorrect
$var = foo( $bar,$baz,$quuz );
```

### Control Structures
Control statements should have one space between the control keyword and opening parenthesis, to distinguish them from function calls. Braces should always be on the same line.

```
// Correct
if ((condition1) || (condition2)) {
	// Do something
} elseif ((condition3) && (condition4)) {
	// Do something
} else {
	// Do something
}
```

Braces should be used on all multiline if, else, elseif conditionals. Braces should not be used if it is a single line. The exception is if any part of the conditional is multiline then the entire block should use braces even if others are single line.

### Arrays
Assignments in arrays should be aligned. When splitting array definitions onto several lines, the last value should also have a trailing comma. This is valid PHP syntax.

```
// Correct
$aArray = array(
	'foo' => 'bar',
	'lorem' => 'ipsum',
);
```

### Comments
Comments should either use C style, `/* */` or standard C++, `//`. Avoid using Perl/shell style comments, `#`. See above for inline documentation.

```
// Correct

/* Correct */

# Incorrect #
```

### PHP Code Tags
Always use `<?php ?>` to delimit PHP code and never the shorthand `<? ?>`.

### Readability
Related lines of code should be grouped into blocks, separated from each other to keep readability as high as possible. The definition of "related" will of course vary on the code.

```
// Correct
if ($foo)
	$bar = 1;

if ($pinky)
	$brain = 1;

// Incorrect
if ($foo)
	$bar = 1;
if($pinky)
	$brain = 1;
```
