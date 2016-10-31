# Input Kludge

`Input Kludge` is a probem in software design in which user input is not correctly handled. This term applies both to valid inputs being falsely rejected as well as bad input being accepted. This can result from a poor user interface.

## Problems

Some of the largest breaches in enterprise security have been due to input kludge issues, when SQL was input into a user populated field and then executed on a server. Ad-hoc input validation routines may point to input kludge but it does not nessarily mean that there is a problem. 

## Testing

The easiest and most simple test for input kludge is "facerolling" or "mashing" the keyboard to generate large garbage input. This is problematic for repeatability, however, and it is common to task UX engineers to attempt to cooerce the program to accept bad input. Automated testing using "fuzzing" generates random code snippets as well as random input to test against the input field. This is the most common practice when testing for Input Kludge.

## Solution

A common solution for Input Kludge is field Validation. Often the provided input is parsed through a series of regular expressions and algorithms to determine if it contains bad input before it is accepted and saved by the program. If the input is bad, it is rejected. 

## For your consideration

```c++
#include <iostream>
using namespace std;

int main(){
  int arr[11] = {0,1,2,3,4,5,6,7,8,9,10};
  int in;
  cout << "ENTER A NUMBER, 0-10: " << endl;
  cin >> in;
  cout << "You selected: " << arr[in] << endl;
  cout << "Executed Succesfully" << endl;
  return 0;
}
```
What values will this program work for? What will hapen if we use bad input? Lets find out!

## Sources
https://www.owasp.org/index.php/Fuzzing
https://sourcemaking.com/antipatterns/input-kludge
https://en.wikipedia.org/wiki/Input_kludge
https://en.wikipedia.org/wiki/Fuzz_testing
