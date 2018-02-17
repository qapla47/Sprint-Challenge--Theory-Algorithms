# Answers to Algorithm section

## Exercise I
1. O(n) - Linear
  object assignment and basic math are constants, the while loop is Linear
    > a = 0;                // constant
    > while (a < n *n *n)   // O(n^3) \
    >> a = a + n *n         // O(n^2) / divide the two for O(n)

2. O(Log n) - Logarithmic
  the i assignments is constant, the while loop has two equality statements for On, the i is dropping by half making it Log n
    > i = array.length -1             // constant
    > while (array[i] > x && i >= 0)  // O(n)
    >> i = i/2                        // Log n

3. O(sqrt n) - Square root of n
  the sum assignment and incrementers are constants
  first loop is square root, the remaining are constants
    > sum = 0;                              // constant
    > for (i = 0; i < Math.sqrt(n)/2; i++)  // square root of n
    >> for (j = i; j < 8+j; j++)            // execute 8 times - constant
    >>> for (k = j; k < 8+j; k++)           // execute 8 times - constant
    >>>> sum++                              // constant

4. O(n Log n) - Linearithmic/ log linear
  again, sum assignment and incrementing are constants
  each loop is is logarithmic as it increases by 2, the second is linear but nested, so OnLogn
    > sum = 0                     // constant
    > for (i = 1; i < n; i *=2)   // O(Log n)   \
    >> for (j = 0; j < n; j++)    // O(n)       / O(n log n)
    >>> sum++                     // constant

5. O(n^3) - Cubic
  again, two constants which are dropped
  the first three loops are linear, the last is constant
    > sum = 0                           // constant
    > for (i = 0; i < n; i++)           // O(n) ------
    >> for (j = i +1; j < n; j++)       // O(n)       | O(n^3)
    >>> for (k = j+1; k < n; k++)       // O(n) ------
    >>>> for (l = k+1; l < 10+k; l++)   // run 9 times - constant
    >>>>> sum++                         // constant

6. O(n) - Linear
  each call to bunnyEars results in a further call to bunnyEars
    > bunnyEars = function(bunnies)       // function declaration is constant
    >> if (bunnies === 0) return 0        // logical comparison is constant
    >> return 2 + bunnyEars(bunnies - 1)  // recursive call iterates is 1, the 2 is a constant O(n)

7. O(n) - Linear
  same as above, each call to search results in a further call to search
    > search = function(array, arraySize, target)       // function declaration is constant
    >> if (arraySize > 0)                               // equality statement is constant
    >>> if (array[arraySize-1] === target) return true  // equality statement is constant
    >>> else return search(array, arraySize-1, target)  // recursive call actually iterates by 1 O(n)
    >> return false                                     // return is constant

  The last two, had they recursed twice (like mathematical formula for fibonacci), would have been exponential. 

## Exercise II

1. Given an array a of n numbers, design a linear running time algorithm to find the max value of: a[j] - a[i], where j >= i.
  A function who has a counter and a single loop with an equality statement
  track min and max values - return min from max
    > function getValues(a) {
    >> let max = a[0], let min = a[0];
    >> for (let i = 0; i < a.length; i++) {
    >>> if (a[i] < min) {
    >>>> min = a[i];
    >>> }
    >>> if (a[i] > max) {
    >>>> max = a[i];
    >>> }
    >> } return max - min;
    > }

    The two if statements above could also be condensed and written:
    a[i] < min ? min = a[i] : a[i] > max ? max = a[i] : i;

2. Suppose that you have an n-story building and plenty of eggs. Suppose also that an egg is broken if it is thrown off floor f or higher, and unbroken otherwise. Devise a strategy to determine the value of f such that the number of dropped eggs is minimized.
  Using a tree structure, your starting node is your total floors divided by two rounding down
  While you're floor is greater than 0 [indicating the ground floor] & you haven't tested this floor
  Drop the egg
    If the egg breaks, move left
      if the previous node was the root node (L)
        Current position divided by two rounding down
      If previous node was NOT the root node, and the previous egg broke (L,L)
        Current - (Current position divided by two rounding down)
      If the previous node was NOT the root node, and the previous egg didn't break (R,L)
        Current + ((Previous - current) divided by two)
    If the egg doesn't break, move right
      If the previous node was the root node (R)
        Current + (Max - Current) divided by two
      If the previous node is NOT the root node, and the previous egg broke (L,R)
        Current - ((Current - previous) divided by two)
      If the previous node is NOT the root node, and the previous egg didn't break (R,R)
        Current + (Max - current) divided by two

![tree construction](/tree.png)
