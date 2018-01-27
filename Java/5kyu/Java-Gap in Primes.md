# Gap in Primes(质数间隔)
# 题目
The prime numbers are not regularly spaced. For example from 2 to 3 the gap is 1. From 3 to 5 the gap is 2. From 7 to 11 it is 4. Between 2 and 50 we have the following pairs of 2-gaps primes: 3-5, 5-7, 11-13, 17-19, 29-31, 41-43

A prime gap of length n is a run of n-1 consecutive composite numbers between two successive primes (see: http://mathworld.wolfram.com/PrimeGaps.html).

We will write a function gap with parameters:

g (integer >= 2) which indicates the gap we are looking for

m (integer > 2) which gives the start of the search (m inclusive)

n (integer >= m) which gives the end of the search (n inclusive)

In the example above gap(2, 3, 50) will return [3, 5] or (3, 5) or {3, 5} which is the first pair between 3 and 50 with a 2-gap.

So this function should return the first pair of two prime numbers spaced with a gap of g between the limits m, n if these numbers exist otherwise nil or null or None or Nothing (depending on the language).

In C++ return in such a case {0, 0}. In F# return [||]. In Kotlin return []

#Examples: gap(2, 5, 7) --> [5, 7] or (5, 7) or {5, 7}

gap(2, 5, 5) --> nil. In C++ {0, 0}. In F# [||]. In Kotlin return[]`

gap(4, 130, 200) --> [163, 167] or (163, 167) or {163, 167}

([193, 197] is also such a 4-gap primes between 130 and 200 but it's not the first pair)

gap(6,100,110) --> nil or {0, 0} : between 100 and 110 we have 101, 103, 107, 109 but 101-107 is not a 6-gap because there is 103 in between and 103-109 is not a 6-gap because there is 107in between.

```
    import java.util.Arrays;

    class GapInPrimes {
        
        public static long[] gap(int g, long m, long n) {
            // your code
        }
    }
```
# 测试用例
```
    import org.junit.Test;
    import static org.junit.Assert.assertEquals;
    import org.junit.runners.JUnit4;

    // TODO: Replace examples and use TDD development by writing your own tests

    public class SolutionTest {
        @Test
        public void testSomething() {
            // assertEquals("expected", "actual");
        }
    }
```
# 解析
    prime:质数
    质数：在大于1的自然数中，除了1和它本身以外不会再有其它因数的数称为质数。从2开始，2是最小的质数
    题目要返回[m,n]之间，第一对质数之间的差是g的组合，而且m和n之间不能再有其他的质数出现，如果没有符合要求的组合，则返回null。
    例如gap(6,100,110)，虽然有[101,107]符合101和107是质数，而且差是6，但是101和107之间存在一个质数103。
# 答案
```
    public static long[] gap(int g, long m, long n) {
        long[] a = null;
        one:
        for (long i = m; i <= n; i++) {
            if (isPrime(i) && isPrime(i + g) && (i + g <= n)) {
                for (long j = i + 1; j < i + g; j++) {
                    if (isPrime(j)) {
                        continue one;
                    }
                }
                a = new long[2];
                a[0] = i;
                a[1] = i + g;
                break;
            }
        }
        return a;
    }
    public static boolean isPrime(long n) {
        for (int i = 2; i < n / 2; i++) {
            if (n % i == 0) {//not prime
                return false;
            }
        }
        return true;
    }
```
---
    记录下上一个质数a，然后求得下一个质数b，如果a-b=g，则返回[a,b]
```
    public static long[] gap(int g, long m, long n) {
        long last = Long.MIN_VALUE;
        for (long i = m; i < n; i++) {
            if (isPrime(i)) {
                if (i - last == g) {
                    return new long[]{last, i};
                }
                last = i;
            }
        }

        return null;
    }

    private static boolean isPrime(long i) {
        for (long j = 2; j < i / 2; j++) {
            if (i % j == 0) return false;
        }
        return true;
    }
```