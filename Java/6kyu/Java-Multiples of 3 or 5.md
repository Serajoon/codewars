# Multiples of 3 or 5(3或5的倍数)
# 题目
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Finish the solution so that it returns the sum of all the multiples of 3 or 5 below the number passed in. 
如果我们列出所有低于10的自然数是3或5的倍数，我们得到3，5，6和9.这些倍数的总和是23。

完成解决方案，以便返回低于传入数字的3或5的所有倍数的总和。
```
    public class Solution {
        public int solution(int number) {
            //TODO: Code stuff here
        }
    }

```
# 测试用例
```
    import org.junit.Test;
    import static org.junit.Assert.assertEquals;

    public class SolutionTest {
        @Test
        public void test() {
            assertEquals(23, new Solution().solution(10));
        }
    }
```
# 答案
求3或者5的倍数，如果使用for循环，则当数量很大时，效率会非常低，考虑是求倍数，则利用等差数列(1+n)*n/2。分别求3和5的等差数列f(3)+f(5)。由于3和5的公倍数被算了两次，同事还要减去f(15)
```
    public class Solution {
        public int solution(int number) {
            return sumOf(number, 3) + sumOf(number, 5) - sumOf(number, 15);
        }
        public int sumOf(int number, int n) {
            int a = (number - 1) / n;
            if (a < 1) {
                return 0;
            } else {
                return (1 + a) * a * n / 2;
            }
        }
    }
```
---
```
    import java.util.stream.IntStream;
    public class Solution {
        public int solution(int number) {
            return IntStream.range(0, number)
                            .filter(n -> (n % 3 == 0) || (n % 5 == 0))
                            .sum();
        }
    }
```