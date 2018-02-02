# Find the smallest
# 题目
You have a positive number n consisting of digits. You can do at most one operation: Choosing the index of a digit in the number, remove this digit at that index and insert it back to another place in the number.

Doing so, find the smallest number you can get.

### Task: Return an array or a tuple or a string depending on the language (see "Sample Tests") with

1) the smallest number you got
2) the index i of the digit d you took, i as small as possible
3) the index j (as small as possible) where you insert this digit d to have the smallest number.

### Example:

smallest(261235) --> [126235, 2, 0] or (126235, 2, 0) or "126235, 2, 0"
126235 is the smallest number gotten by taking 1 at index 2 and putting it at index 0

smallest(209917) --> [29917, 0, 1] or ...

[29917, 1, 0] could be a solution too but index `i` in [29917, 1, 0] is greater than 
index `i` in [29917, 0, 1].
29917 is the smallest number gotten by taking 2 at index 0 and putting it at index 1 which gave 029917 which is the number 29917.

smallest(1000000) --> [1, 0, 6] or ...
```
    public class ToSmallest {
        
        public static long[] smallest(long n) {
            // your code
        }
    }
```
# 测试用例
```
    import static org.junit.Assert.*;
    import java.util.Arrays;
    import org.junit.Test;

    public class ToSmallestTest {

        private static void testing(long n, String res) {
            assertEquals(res, 
                        Arrays.toString(ToSmallest.smallest(n)));
        }
        @Test
        public void test() {
            System.out.println("Basic Tests smallest");
            testing(261235, "[126235, 2, 0]");
            testing(209917, "[29917, 0, 1]");
            testing(285365, "[238565, 3, 1]");
            testing(269045, "[26945, 3, 0]");
            testing(296837, "[239687, 4, 1]");
        }
    }
```
# 答案
```
    public static long[] smallest(long n) {
        char[] chars = String.valueOf(n).toCharArray();
        long[] result = new long[3];
        long r = Long.MAX_VALUE;
        long index1 = Long.MAX_VALUE;
        long index2 = Long.MAX_VALUE;
        for (int i = 0; i < chars.length; i++) {
            java.util.ArrayList<Character> characters = longtoArrayList(n);
            Character remove = characters.remove(i);
            for(int j=0;j<=characters.size();j++){
                characters.add(j,remove);
                StringBuffer sb = new StringBuffer();
                for(Character c:characters){
                    sb.append(c);
                }
                long l = new java.math.BigInteger(sb.toString()).longValue();
                if(l<r){
                    r=l;
                    index1=i;
                    index2=j;
                }
                characters.remove(j);
            }
        }
        result[0]=r;
        result[1]=index1;
        result[2]=index2;
        return result;
    }

    public static java.util.ArrayList<Character> longtoArrayList(long n) {
        char[] chars = String.valueOf(n).toCharArray();
        java.util.ArrayList<Character> list = new java.util.ArrayList<>();
        for (int i = 0; i < chars.length; i++) {
            list.add(chars[i]);
        }
        return list;
    }
```
```
    public static long[] smallest(long n) {
        long min = n;
        int index1 = 0;
        int index2 = 0;
        String number = String.valueOf(n);
        for (int i = 0; i < number.length(); i++) {
            for (int j = 0; j < number.length(); j++) {
                if (i != j && making(number, i, j) < min) {
                    min = making(number, i, j);
                    index1 = i;
                    index2 = j;
                }
            }
        }
        return new long[]{min, index1, index2};
    }

    public static long making(String s, int i, int j) {
        StringBuilder sb = new StringBuilder(s);
        char c = sb.charAt(i);
        sb.deleteCharAt(i);
        sb.insert(j, c);

        return Long.valueOf(sb.toString());
    }
```