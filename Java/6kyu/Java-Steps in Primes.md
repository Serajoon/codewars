# Steps in Primes
# 题目
The prime numbers are not regularly spaced. For example from 2 to 3 the step is 1. From 3 to 5 the step is 2. From 7 to 11 it is 4. Between 2 and 50 we have the following pairs of 2-steps primes:

3, 5 - 5, 7, - 11, 13, - 17, 19, - 29, 31, - 41, 43

We will write a function step with parameters:

g (integer >= 2) which indicates the step we are looking for,
m (integer >= 2) which gives the start of the search (m inclusive),
n (integer >= m) which gives the end of the search (n inclusive)
In the example above step(2, 2, 50) will return [3, 5] which is the first pair between 2 and 50 with a 2-steps.

So this function should return the **first pair** of the two prime numbers spaced with a step of g between the limits m, n if these g-steps prime numbers exist otherwise nil or null or None or Nothing or [] or "0, 0" or {0, 0} (depending on the language).

## Examples:

step(2, 5, 7) --> [5, 7] or (5, 7) or {5, 7} or "5 7"

step(2, 5, 5) --> nil or ... or [] in Ocaml or {0, 0} in C++

step(4, 130, 200) --> [163, 167] or (163, 167) or {163, 167}

See more examples for your language in "RUN"
Remarks:
([193, 197] is also such a 2-steps primes between 130 and 200 but it's not the first pair).

step(6, 100, 110) --> [101, 107] though there is a prime between 101 and 107 which is 103; the pair 101-103 is a 2-step.

#Notes: The idea of "step" is close to that of "gap" but it is not exactly the same. For those interested they can have a look at http://mathworld.wolfram.com/PrimeGaps.html.

A "gap" is more restrictive: there must be no primes in between (101-107 is a "step" but not a "gap". Next kata will be about "gaps":-).
```
class StepInPrimes {
    
    public static long[] step(int g, long m, long n) {
        // your code
    }
}
```
# 测试用例
```
import static org.junit.Assert.*;
import java.util.Arrays;
import org.junit.Test;

public class StepInPrimesTest {
    @Test
    public void test() {
        System.out.println("Fixed Tests");        
        assertEquals("[101, 103]", Arrays.toString(StepInPrimes.step(2,100,110)));
        assertEquals("[103, 107]", Arrays.toString(StepInPrimes.step(4,100,110)));
        assertEquals("[101, 107]", Arrays.toString(StepInPrimes.step(6,100,110)));
        assertEquals("[359, 367]", Arrays.toString(StepInPrimes.step(8,300,400)));
        assertEquals("[307, 317]", Arrays.toString(StepInPrimes.step(10,300,400)));
    }
}
```
# 答案
（1）从2开始，2是最小的质数。

（2）除了2之外的偶数全都不是质数，因为除了1和自身之外它们还能被2整除。若为大于2的奇数，则进入下一步继续判断。

（3）将其开方，若从3到开方向下取整之间的所有奇数都不能将其整除，则说明该数为质数。
```
    public static long[] step(int g, long m, long n) {
        long[] a = new long[2];
        for (long i = m; i <= n; i++){
            if(isPrime(i)&&isPrime(i+g)&&(i+g)<=n) {
                a[0]=i;
                a[1]=i+g;
                return a;
            }
        }
        return null;
    }
    //判断是否是质数
    public static boolean isPrime(long a) {
        boolean result = true;
        for (long i = 2; i <= a / 2; i++) {
            if (a % i == 0) {
                result = false;
                break;
            }
        }
        return result;
    }
    public static boolean isprime(long a) {
        if (a < 2 || a % 2 == 0) {
            return false;
        } else if (a == 2) {
            return true;
        } else {
            for (long i = 3; i <= Math.sqrt(a); i++) {
                if (a % i == 0) {
                    return false;
                }
            }
            return true;
        }
    }
```
---
```
    public static long[] step(int g, long m, long n) {
        long[] res = new long[2];
        long i = m;
        while (i <= n - g) {
            if (prime(i) && prime(i + g)) {
                res[0] = i;
                res[1] = i + g;
                return res;
            }
            i++;
        }
        return null;
    }
    
    private static boolean prime(long n) {
        if (n == 2) return true;
        else if ((n < 2) || (n % 2 == 0)) return false;
        else {
            for (long i = 3; i <= Math.sqrt(n); ++i) {
                if (n % i == 0) return false;
            }
            return true;
        }
    }
```