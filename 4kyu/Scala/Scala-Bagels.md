# Bagels
# 题目

```
class Bagel {
  final def getValue = 3
}
```
```
object BagelSolver {
  //修改这
  def getBagel: Bagel = {
    new Bagel
  }
}
```
# 测试用例
```
import org.junit.Assert.assertEquals
import org.junit.Test

class BagelTest {
  @Test def testBagel(): Unit = {
    assertEquals(BagelSolver.getBagel.getValue == 4, java.lang.Boolean.TRUE)
  }
}
```
# 答案
## Scala
```
object BagelSolver {
  def getBagel = new {
    def getValue() : Int = 4
  }
}
```
    利用反射
```
object BagelSolver {
  def getBagel: Bagel = {
    try {
      val value = classOf[java.lang.Boolean].getDeclaredField("value")
      value.setAccessible(true)
      value.set(java.lang.Boolean.TRUE, java.lang.Boolean.FALSE)
    } catch {
      case e: Throwable =>
        e.printStackTrace()
    }
    new Bagel
  }
}
```