---
title: Manipulating Strings
description: How to manipulate strings and create substrings from strings etc.
published: true
date: 2022-10-10T18:09:10.273Z
tags: bash, string-manipulation, strings
editor: markdown
dateCreated: 2022-10-10T18:09:10.273Z
---

# Print the Length of the String

````bash
example=Value

echo ${#example}
````

**Output: 5**

# Extract a Substring from String

Returns a substring starting from $position till end
````bash
${string:position}
````

Returns a substring of $length characters starting from $position.
````bash
${string:position:length}
````

# Remove Characters from the End of a String

````bash
example1=someexampledomain.com
shortExample="${example1::-4}"

echo "${shortExample}"
````

**Output: someexampledomain**

# Using Sed Command to Remove Characters


### Remove Characters From Beginning of String
````bash
echo "ExampleString" | sed 's/^.......//'
````

**Returns: String**

<br>

### Remove Characters From End of String
````bash
echo "ExampleString" | sed 's/......$//'
````

**Returns: Example**

<br>


