# Bagels
# 题目

```
public class Bagel {
    public final int getValue() {
        return 3;
    }
}
```
```
public class BagelSolver {
  public static Bagel getBagel() {
    // TODO : Implement me.
    return new Bagel();
  }
}
```
# 测试用例
```
import org.junit.Test;
import static org.junit.Assert.assertEquals;
import org.junit.runners.JUnit4;

public class BagelTest {

    @Test
    public void testBagel() {
        Bagel bagel = BagelSolver.getBagel();
        //修改代码使下面成立
        assertEquals(bagel.getValue() == 4,java.lang.Boolean.TRUE);
    }

}
```
# 答案
## Java
```
import java.lang.reflect.Field;
public class BagelSolver {

  public static Bagel getBagel() {
        Class<Boolean> booleanClass = Boolean.class;
        try {
            Field value = booleanClass.getDeclaredField("value");
            value.setAccessible(true);
            value.set(Boolean.TRUE, Boolean.FALSE);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return new Bagel();
  }
}
```

## Scala
```
object BagelSolver {
  def getBagel = new {
    def getValue() : Int = 4
  }
}
```