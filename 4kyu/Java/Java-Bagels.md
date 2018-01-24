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
    因为final方法不能被覆盖，所以没法通过修改代码来解决。bagel.getValue() == 4肯定为false，但是要使assertEquals成立，只能使用反射机制，将java.lang.Boolean.TRUE的值改为false，则assertEquals(false,false)成立
    public static final Boolean TRUE = new Boolean(true);
    由于Boolean的value定义为private final boolean value;所以必须要setAccessible(true)，取消java语言访问检查
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