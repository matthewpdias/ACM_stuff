# LCS
## Longest common subsequence
---

## Introduction
Given a series of strings, find the longest common subsequence among them all. A subsequence is a sequence that appears in the same order, but is not necessarily consequtive.

To give you an idea, the strings: `ABCD` and `AEFD` have the LCS of `AD` 

A string of length *n* will have 2<sup>*n*</sup> different possible substrings.

This is a very important problem in computing, and the solution is the fundamental basis for the diff utility which I'm sure you are all familiar with.

## Application

Given two different strings: `AGGTAB` and `GXTXAYB` find the longest common substring between the two.

How would you approach this? The Naive approach is to split the two strings into all of the possible substrings.
Why is this a bad idea? What is the time complexity?

```c++
/* A Naive recursive implementation of LCS problem */
#include<bits/stdc++.h>
 
int max(int a, int b);
 
/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
int lcs( char *X, char *Y, int m, int n )
{
   if (m == 0 || n == 0)
     return 0;
   if (X[m-1] == Y[n-1])
     return 1 + lcs(X, Y, m-1, n-1);
   else
     return max(lcs(X, Y, m, n-1), lcs(X, Y, m-1, n));
}
 
/* Utility function to get max of 2 integers */
int max(int a, int b)
{
    return (a > b)? a : b;
}
 
/* Driver program to test above function */
int main()
{
  char X[] = "AGGTAB";
  char Y[] = "GXTXAYB";
 
  int m = strlen(X);
  int n = strlen(Y);
 
  printf("Length of LCS is %d\n", lcs( X, Y, m, n ) );
 
  return 0;
}
```

This solution has the time complexity of O(2<sup>*n*</sup>)

## A different approach

Dynamic programming can be applied tho this problem and a much better time complexity can be acchieved. A bottom-up approach is used to build the LCS.

```c++
/* Dynamic Programming C/C++ implementation of LCS problem */
#include<bits/stdc++.h>
  
int max(int a, int b);
  
/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
int lcs( char *X, char *Y, int m, int n )
{
   int L[m+1][n+1];
   int i, j;
  
   /* Following steps build L[m+1][n+1] in bottom up fashion. Note 
      that L[i][j] contains length of LCS of X[0..i-1] and Y[0..j-1] */
   for (i=0; i<=m; i++)
   {
     for (j=0; j<=n; j++)
     {
       if (i == 0 || j == 0)
         L[i][j] = 0;
  
       else if (X[i-1] == Y[j-1])
         L[i][j] = L[i-1][j-1] + 1;
  
       else
         L[i][j] = max(L[i-1][j], L[i][j-1]);
     }
   }
    
   /* L[m][n] contains length of LCS for X[0..n-1] and Y[0..m-1] */
   return L[m][n];
}
  
/* Utility function to get max of 2 integers */
int max(int a, int b)
{
    return (a > b)? a : b;
}
  
/* Driver program to test above function */
int main()
{
  char X[] = "AGGTAB";
  char Y[] = "GXTXAYB";
  
  int m = strlen(X);
  int n = strlen(Y);
  
  printf("Length of LCS is %d\n", lcs( X, Y, m, n ) );
 
  return 0;
}
```
The dynamic programming solution above has a time complexity of O(mn).

animation availiable [here](https://www.cs.usfca.edu/~galles/visualization/DPLCS.html)
