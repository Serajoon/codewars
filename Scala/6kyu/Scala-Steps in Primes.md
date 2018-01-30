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

（1）从2开始，2是最小的质数。

（2）除了2之外的偶数全都不是质数，因为除了1和自身之外它们还能被2整除。若为大于2的奇数，则进入下一步继续判断。

（3）将其开方，若从3到开方向下取整之间的所有奇数都不能将其整除，则说明该数为质数。
```
class StepInPrimes {
    
    public static long[] step(int g, long m, long n) {
        // your code
    }
}
```
# 测试用例
```
import org.junit.Assert._
import org.junit.Test

class StepInPrimesTest {
  @Test
  def test(): Unit = {
    println("Fixed Tests")
    assertEquals("(101,103)", StepInPrimes.step(2, 100, 110))
    
    assertEquals("(30109,30113)", StepInPrimes.step(4, 30000, 100000))
    
    //assertEquals("", StepInPrimes.step(11, 30000, 100000))
  }

}
```
# 答案

```
    def step(g: Int, m: Long, n: Long): String = {
        val stepPrimes = (for (i <- (m to n).toStream
        if isPrime(i)
        if i + g <= n
        if isPrime(i + g)
        ) yield (i, i + g)).headOption

        stepPrimes match {
            case None => ""
            case Some(x) => x.toString()
        }
    }

    def isPrime(n: Long): Boolean = !List.range(2, math.sqrt(n).toInt + 1).exists(x => (n % x) == 0)
```