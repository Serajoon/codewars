# Multiples of 3 or 5(3或5的倍数)
# 题目
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Finish the solution so that it returns the sum of all the multiples of 3 or 5 below the number passed in. 
如果我们列出所有低于10的自然数是3或5的倍数，我们得到3，5，6和9.这些倍数的总和是23。

完成解决方案，以便返回低于传入数字的3或5的所有倍数的总和。
```
    object MultiplesOf3Or5 {   
        def solution(number: Int): Long = ???
    }

```
# 测试用例
```
    import org.junit.runner.RunWith
    import org.scalatest.junit.JUnitRunner
    import org.scalatest.FunSpec

    import scala.util.Random

    @RunWith(classOf[JUnitRunner])
    class MultiplesOf3Or5Suite extends FunSpec {
        
        import MultiplesOf3Or5._
        
        describe("Multiples of 3 or 5") {
            it("should handle basic cases") {
                assert(solution(10) === 23)
                assert(solution(20) === 78)
            }
        }
    }
```
# 答案
求3或者5的倍数，如果使用for循环，则当数量很大时，效率会非常低，考虑是求倍数，则利用等差数列(1+n)*n/2。分别求3和5的等差数列f(3)+f(5)。由于3和5的公倍数被算了两次，同事还要减去f(15)
```
    object MultiplesOf3Or5 {   
        def solution(number: Long):Long = {
            val result: Long = a(number, 3) + a(number, 5) - a(number, 15)
            result
        }

        def a(num: Long, n: Int): Long = {
            var result: Long = 0L
            val l: Long = (num - 1) / n
            if (l >= 1) {
            result = (1 + l) * l * n / 2
            }
            result
        }
    }
```
---
利用等差数列
```
    object MultiplesOf3Or5 {   
        def solution(number: Int): Long = {
            def sumOf(k: Long): Long = {
                val n = (number - 1) / k
                k * n * (n + 1) / 2
            }
            
            sumOf(3) + sumOf(5) - sumOf(15)
        }
    }
```
---
利用scala的view的惰性求值，List用foldLeft求和
```
    object MultiplesOf3Or5 {   
    def solution(number: Int): Long =
        (1 until number).view.filter(x => x % 3 == 0 || x % 5 == 0).foldLeft(0L)(_ + _)
    }
```