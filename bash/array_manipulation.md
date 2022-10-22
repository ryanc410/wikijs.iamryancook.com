---
title: Manipulating Arrays
description: Different ways to manipulate an array inside the BASH shell
published: true
date: 2022-10-22T13:36:33.246Z
tags: bash, arrays, manipulate
editor: markdown
dateCreated: 2022-10-22T13:36:33.246Z
---

# Print All Array Elements
````bash
arr=(elem1 elem2 elem3 elem4)

echo ${arr[@]}       
echo ${arr[*]}        
echo ${arr[@]:0}    
echo ${arr[*]:0}

# Each one of the previous commands have the exact same output:

elem1 elem2 elem3 elem4
````

# Print First Element
````bash
echo ${arr[0]}
echo ${arr}

# Output
elem1
````

# Print Specified Element
````bash
echo ${arr[3]} 
echo ${arr[1]}

# Output
elem4
elem2
````

# Print elements from a particular index
````bash
echo ${arr[@]:0}    
echo ${arr[@]:1}   
echo ${arr[@]:2}    
echo ${arr[0]:1}

# Output
elem1 elem2 elem3 elem4
elem2 elem3 elem4
elem3 elem4
lem1
````

# Print elements in range
````bash
echo ${arr[@]:1:4}
echo ${arr[@]:2:3}    
echo ${arr[0]:1:3} 

# Output
elem2 elem3 elem4
elem3 elem4
lem
````

# Print the Length of Particular element
````bash
echo ${#arr[0]} 
echo ${#arr}  

# Output
5
5
````

# Size of an Array
````bash
echo ${#arr[@]} 
echo ${#arr[*]}   

# Output
4
4
````

# Search in Array
````bash
echo ${arr[@]/*[aA]*/}

# Output
elem1 elem2 elem3 elem4
````