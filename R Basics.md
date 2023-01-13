# R Basics

- **Calculation**

  The basic operations are `*,+,-,/,^`.

  ```R
  > 2+3
  > 2*3
  > 2/3    		 # 0.6666667
  > 2^3		 		 # 8
  > 2*(3+1)^2  # 32: 2 * (4^2) (^ has a higher priority)
  ```

- **Assignment:** `x = 3` or `x <- 3`

- **Vectors**: A vector is a type of list (of numbers, characters, ...) --> `c()`

  ```R
  ## 1. Initializations
  c(1, 2, 3, 4)   							 # 1 2 3 4
  x = c(1.1, 0.0, 3.14, 2.718)   # 1.100 0.000 3.140 2.718 (same number of digits)
  x <- c(1.1, 0.0, 3.14, 2.718) 
  
  # Sequences of integers (in-order + both inclusive)
  1:4				# 1 2 3 4 
  9:2				# 9 8 7 6 5 4 3 2 1
  
  # A long vector will be displayed over several lines. At the start of each line in brackets is the index of the first entry on that line.
  > x = 1:40
  > x
   [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 
   [15] 15 16 17 18 19 20 21 22 23 24 25 26 27 28 
   [29] 29 30 31 32 33 34 35 36 37 38 39 40
  
  ## 2. Vector Arithmetic --> broadcasting
  > x = c(1,3,5)
  > x + 7.1
  [1]  8.1 10.1 12.1
  > x = c(1,3,5)
  > 7*x
  [1]  7 21 35
  > x/7
  [1] 0.1428571 0.4285714 0.7142857
  > 7/x
  [1] 7.000000 2.333333 1.400000
  > x^6
  [1]     1   729 15625
  > x^7
  [1]     1  2187 78125
  > 7^x
  [1]     7   343 16807
  # applied to two vectors: x + y; x * y; x / y; x ^ y (element-wise)
  
  ## 3. Access Entries
  x[c(1,3,5)]   # access x[1], x[3], x[5]
  x[c(2,2,2,1)] # access x[2], x[2], x[2], x[1] --> multiple times
  x[2:5]				# access x[2], x[3], x[4], x[5]
  
  ## 4. Functions
  sin(1)
  sin(c(1, 2, 3, 4))
  pi
  exp(0)
  
  x = 1:6
  sum(x)		# or: sum(1:6)
  mean(x)   # or: mean(1:6)
  sum(x^2)  # or: sum((1:6)^2)
  ```

- **Matrices**

  --> arrange the entries in a vector into rows and columns

  ```R
  ## 1. Initialization
  # A vector of length 10 can be arranged as a 2x5 or a 5x2 matrix
  x = 1:10
  y = matrix(x, nrow=2, ncol=5)    # 2x5 matrix
  
  > x
   [1]  1  2  3  4  5  6  7  8  9 10
  > y															 
       [,1] [,2] [,3] [,4] [,5]
  [1,]    1    3    5    7    9
  [2,]    2    4    6    8   10
  
  # R builds the matrix by/along column by default, can build by rows
  y = matrix(x, nrow=2, ncol=5, byrow=True)
  
  ## 2. Access Entries
  y[1, 1]
  
  ## 3. Calculations
  
  ```

  

## Attention / Tips

- In R, indices start with 1, not 0 (in Python).
- Calculations in vectors are done element-wisely.

