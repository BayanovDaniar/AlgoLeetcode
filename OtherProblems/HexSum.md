 #Other #JavaScript

#Yandex 

<kbd><span style="color:orange;">#Medium</span> </kbd>


---

**Задача:** Написать функцию для сложения двух очень длинных шестнадцатеричных чисел. Числа настолько велики, что они не помещаются в памяти компьютера как единое целое. Ваш алгоритм должен обрабатывать числа поциферно, подобно тому, как это делается при сложении чисел в столбик.

**Входные данные:**

- `num1` и `num2` - строки, представляющие шестнадцатеричные числа.

**Выходные данные:**

- Строка, представляющая сумму `num1` и `num2` в шестнадцатеричной форме.

**Требования:**

- Не использовать встроенные функции для прямого преобразования больших чисел из одной системы счисления в другую или для их сложения.
- Сложение должно выполняться "в столбик", обеспечивая корректное сложение цифр и перенос излишка в следующий разряд.
- Алгоритм должен корректно обрабатывать ситуации с числами разной длины.
- Обеспечить обработку "переполнения" при сложении (когда сумма цифр превышает базу шестнадцатеричной системы счисления).

---

<kbd><span style="color:red;"> Intuitive</span></kbd>

1.  Сначала строки переворачиваются для удобства итерации от младших к старшим разрядам. 
2. Затем итерация ведется по кратчайшему числу для выполнения поцифрового сложения с учетом переноса в старший разряд. 
3. После завершения сложения с кратчайшим числом аналогичные действия продолжаются для оставшихся разрядов более длинного числа. 
4. Если после завершения всех операций остается перенос, он добавляется в конец результата. 
5. В завершение результат переворачивается обратно и приводится к верхнему регистру для соответствия общепринятому формату шестнадцатеричных чисел.

```java
package Leetcode.Other;  
  
public class HexSum {  
  
    public static void main(String[] args) {  
        // Пример использования  
        String num1 = "1A2B3C4D5E";  
        String num2 = "FEDCBA9876";  
        System.out.println("Сумма: " + hexSum(num1, num2));  
    }  
  
    private static String hexSum(String num1, String num2) {  
        // Переворачиваем строки, чтобы начать сложение с младших разрядов  
        String longNum = new StringBuilder(num1.length() > num2.length() ? num1 : num2).reverse().toString();  
        String shortNum = new StringBuilder(num1.length() <= num2.length() ? num1 : num2).reverse().toString();  
  
        StringBuilder result = new StringBuilder();  
        int carry = 0;  
  
        for (int i = 0; i < shortNum.length(); i++) {  
            int digit1 = Character.digit(longNum.charAt(i), 16);  
            int digit2 = Character.digit(shortNum.charAt(i), 16);  
            int sum = digit1 + digit2 + carry;  
            carry = sum / 16;  
            result.append(Integer.toHexString(sum % 16));  
              
        }  
  
        for (int i = shortNum.length(); i < longNum.length(); i++) {  
            int digit = Character.digit(longNum.charAt(i), 16);  
            int sum = digit + carry;  
            carry = sum / 16;  
            result.append(Integer.toHexString(sum % 16));  
        }  
  
        if (carry > 0) {  
            result.append("1");  
        }  
  
        // Возвращаем результат в прямом порядке  
        return result.reverse().toString().toUpperCase();  
    }  
}```
