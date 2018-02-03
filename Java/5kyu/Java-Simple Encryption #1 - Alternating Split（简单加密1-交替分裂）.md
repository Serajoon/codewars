# Simple Encryption #1 - Alternating Split(简单加密1-交替分裂)
# 题目
For building the encrypted string:
Take every 2nd char from the string, then the other chars, that are not every 2nd char, and concat them as new String.
Do this n times!

### Examples:

"This is a test!", 1 -> "hsi  etTi sats!"
"This is a test!", 2 -> "hsi  etTi sats!" -> "s eT ashi tist!"
Write two methods:

String encrypt(final String text, final int n)

String decrypt(final String encryptedText, final int n)

For both methods:

If the input-string is null or empty return exactly this value!

If n is <= 0 then return the input text.

题目的意思是对于一个字符串

**加密规则** 取出所有偶数位的字符拼成一个字符串A(包括空格符),剩下的将所有剩下的奇数位的字符拼成一个字符字符串B，然后将A和B拼接成一个字符串。

**解密规则** 因为加密后的字符串是源字符串的偶数位字符序列和奇数位字符序列拼接而成的，所以解密的规则就是将字符串分成两部分，然后循环分别取后一部分的字符和前一部分的字符以此累加成为一个新的字符串。
```
    public class Kata {

    public static String encrypt(final String text, final int n) {
        // Your code here
        return null;   
    }
    
    public static String decrypt(final String encryptedText, final int n) {
        // Your code here
        return null;
    }
    
    }
```
# 测试用例
```
import org.junit.Test;
import static org.junit.Assert.*;

    public class ExampleTests {

        @Test
        public void testEncrypt() {
            // assertEquals("expected", "actual");
            assertEquals("This is a test!", Kata.encrypt("This is a test!", 0));
            assertEquals("hsi  etTi sats!", Kata.encrypt("This is a test!", 1));
            assertEquals("s eT ashi tist!", Kata.encrypt("This is a test!", 2));
            assertEquals(" Tah itse sits!", Kata.encrypt("This is a test!", 3));
            assertEquals("This is a test!", Kata.encrypt("This is a test!", 4));
            assertEquals("This is a test!", Kata.encrypt("This is a test!", -1));
            assertEquals("hskt svr neetn!Ti aai eyitrsig", Kata.encrypt("This kata is very interesting!", 1));
        }
            
        @Test
        public void testDecrypt() {
            // assertEquals("expected", "actual");
            assertEquals("This is a test!", Kata.decrypt("This is a test!", 0));
            assertEquals("This is a test!", Kata.decrypt("hsi  etTi sats!", 1));
            assertEquals("This is a test!", Kata.decrypt("s eT ashi tist!", 2));
            assertEquals("This is a test!", Kata.decrypt(" Tah itse sits!", 3));
            assertEquals("This is a test!", Kata.decrypt("This is a test!", 4));
            assertEquals("This is a test!", Kata.decrypt("This is a test!", -1));
            assertEquals("This kata is very interesting!", Kata.decrypt("hskt svr neetn!Ti aai eyitrsig", 1));
        }
            
        @Test
        public void testNullOrEmpty() {
            // assertEquals("expected", "actual");
            assertEquals("", Kata.encrypt("", 0));
            assertEquals("", Kata.decrypt("", 0));
            assertEquals(null, Kata.encrypt(null, 0));
            assertEquals(null, Kata.decrypt(null, 0));
        }
    }
```
# 答案
```
    public static String encrypt(final String text, final int n) {
        if (text == null || text.length() == 0 || n < 0) {
            return text;
        }
        int num = n;
        String result = text;
        while (num > 0) {
            result = en(result);
            num--;
        }
        return result;
    }

    public static String en(String text) {
        StringBuffer sbEven = new StringBuffer();
        StringBuffer sbOdd = new StringBuffer();
        for (int i = 0; i < text.length(); i++) {
            if (i % 2 == 0) {
                sbEven.append(text.charAt(i));
            } else {
                sbOdd.append(text.charAt(i));
            }
        }
        return sbOdd.append(sbEven).toString();
    }

    public static String decrypt(final String encryptedText, final int n) {
        if (encryptedText == null || encryptedText.length() == 0 || n < 0) {
            return encryptedText;
        }
        int num = n;
        String result = encryptedText;
        while (num > 0) {
            result = de(result);
            num--;
        }
        return result;
    }

    public static String de(String text) {
        StringBuffer sb = new StringBuffer();
        int length = text.length();
        int n = text.length() / 2;
        for (int i = n; i < length; i++) {
            sb.append(text.charAt(i));
            if(i - n<n){
                sb.append(text.charAt(i - n));
            }
        }
        return sb.toString();
    }
```
```
    public static String encrypt(final String text, int n) {
        if (n <= 0 || text == null || text.isEmpty()) {
            return text;
        }

        StringBuilder firstPart = new StringBuilder();
        StringBuilder secondPart = new StringBuilder();
        for (int i = 0; i < text.length(); i++) {
            char aChar = text.charAt(i);
            if (i % 2 == 1) {
                firstPart.append(aChar);
            } else {
                secondPart.append(aChar);
            }
        }

        return encrypt(firstPart.append(secondPart).toString(), --n);
    }

    public static String decrypt(final String encryptedText, int n) {
        if (n <= 0 || encryptedText == null || encryptedText.isEmpty()) {
            return encryptedText;
        }

        StringBuilder text = new StringBuilder();
        final int half = encryptedText.length() / 2;
        for (int i = 0; i < half; i++) {
            text.append(encryptedText.charAt(half + i)).append(encryptedText.charAt(i));
        }
        if (encryptedText.length() % 2 == 1) {
            text.append(encryptedText.charAt(encryptedText.length() - 1));
        }

        return decrypt(text.toString(), --n);
    }
```