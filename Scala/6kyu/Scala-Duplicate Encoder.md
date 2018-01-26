# Duplicate Encoder(重复编码器)
# 题目
The goal of this exercise is to convert a string to a new string where each character in the new string is '(' if that character appears only once in the original string, or ')' if that character appears more than once in the original string. Ignore capitalization when determining if a character is a duplicate.

这个练习的目标是把一个字符串转换成一个新的字符串，其中新字符串中的每个字符是'('如果该字符在原始字符串中只出现一次，或')'，如果该字符在原始字符中出现多次 串。 确定字符是否重复时忽略大小写。
Examples:

"din" => "((("

"recede" => "()()()"

"Success" => ")())())"

"(( @" => "))(("
```
object Solution {
  def duplicateEncode(word: String) = {
    // Your code here
  }
}
```
# 测试用例
```
import org.junit.runner.RunWith
import org.scalatest.junit.JUnitRunner
import org.scalatest._
import scala.util.Random
import Solution._

@RunWith(classOf[JUnitRunner])
class duplicateEncodeSuite extends FunSpec {

  val basicExamples = Seq(
    ("din", "((("),
    ("recede", "()()()"),
    ("Success", ")())())"),
    ("(( @", "))((")
  )
  
  basicExamples.foreach { case (decoded, encoded) => 
    it(s"should return ${encoded} for input ${decoded}") {
      assert(duplicateEncode(decoded) == encoded)
    }
  }
}
```
# 答案
```
  def duplicateEncode(word: String) = {
    val a = word.toLowerCase()
    val hashMap: java.util.HashMap[Character, Integer] = new java.util.HashMap[Character, Integer]()
    a.foreach(t => {
      if (hashMap.containsKey(t)) {
        hashMap.put(t, hashMap.get(t) + 1)
      } else {
        hashMap.put(t, 1)
      }
    })
    val array: Array[Char] = a.toCharArray
    val map: Array[Integer] = array.map(t => {
      val a = hashMap.get(t)
      a
    })
    val array1: Array[String] = for (i <- map)
      yield if (i == 1) "(" else ")"
    array1.mkString
  }
```
```
  def duplicateEncode(word: String) = {
    word.map { char =>
      if (word.count(_.toUpper == char.toUpper) > 1) ')' else '('
    }
  }
```
```
  def duplicateEncode(word: String) = {
    val wordLower = word.toLowerCase
    val charCounts = wordLower.groupBy(identity).mapValues(_.size)
    wordLower.map(c => if (charCounts(c) > 1) ')' else '(')
  }
```