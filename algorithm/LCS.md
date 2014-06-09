Date: 2014-06-09
Title: 最长公共子序列 
Tags: LCS
Category: Algorithm

-------------------------

```C
#include <iostream>
#include <algorithm>
#include <string>
#include <cstdio>
#include <memory.h>
using namespace std;
const int MAX = 100;

int lcs_length(const char *x, const char *y, int xlen, int ylen, int (*c)[MAX])
{
    int i, j;
    for(i = 1; i <= xlen; ++i)
    {
        for(j = 1; j <= ylen; ++j)
        {
            if(x[i - 1] == y[j - 1])    // remember array start from 0
                c[i][j] = c[i - 1][j - 1] + 1;
            else if(c[i - 1][j] >= c[i][j - 1])
                c[i][j] = c[i - 1][j];
            else
                c[i][j] = c[i][j - 1];
        }
    }
    return 0;
}

int print_lcs(const int (*C)[MAX], const char *x, int i, int j, string &s)
{
   if(i == 0 || j == 0) 
       return 0;
   if(C[i][j-1] == C[i-1][j] && C[i][j] > C[i-1][j-1] && C[i][j] != C[i][j-1] && C[i][j] != C[i-1][j])
   {
       s += x[i - 1];
       print_lcs(C, x, i - 1, j - 1, s);
   }
   else if(C[i][j-1] > C[i-1][j])
       print_lcs(C, x, i, j - 1, s);
   else
       print_lcs(C, x, i - 1, j, s);
}
```
