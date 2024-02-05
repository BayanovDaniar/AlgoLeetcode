#TwoPointers #String

#Yandex 

#Easy

---

Удалить все включения смайлов формата :-) или :-(, которые могут продолжаться, например `:-))))`или `:-(((`, скобки должны совпадать друг с другом в одном смайле, например `:-))()` оставит ().

---
Проходимся по строке в поиске `:-`, дальше смотрим что идет за ним и в цикле обрабатываем все одинаковые скобочки(не добавляем их в новую строку, включая `:-`, остальные символы остаются неизменными.

Более предпочтительное решение. 

``` java
package YandexInterview;

// Euclid
public class Smiles {
    public static void main(String[] args) {
    }

    public static String removeSmileys2(String s) {
        StringBuilder result = new StringBuilder();
        for (int i = 0; i < s.length();) {
            if (s.startsWith(":-", i)) {
                int skip = i + 2; // Пропускаем начало смайлика ":-"
                // Определяем тип скобок для удаления
                if (skip < s.length() && (s.charAt(skip) == '(' || s.charAt(skip) == ')')) {
                    char bracketType = s.charAt(skip);
                    while (skip < s.length() && s.charAt(skip) == bracketType) {
                        skip++;
                    }
                    i = skip; // Перемещаем индекс за последнюю скобку
                    continue; // Продолжаем со следующего символа после смайлика
                }
            }
            // Добавляем текущий символ к результату, если он не часть смайлика
            result.append(s.charAt(i));
            i++; // Переходим к следующему символу
        }
        return result.toString();
    }
```

``` java
    public static String removeSmileys(String s) {
        StringBuilder result = new StringBuilder();
        int i = 0;

        while (i < s.length()) {
            if (i + 1 < s.length() && s.charAt(i) == ':' && s.charAt(i + 1) == '-') {
                i += 2; // Пропускаем ":-"
                boolean smileyDetected = false;


                if (i < s.length() && (s.charAt(i) == '(' || s.charAt(i) == ')')) {
                    smileyDetected = true; // Обнаружен полный смайлик
                    char currentChar = s.charAt(i);

                    // Пропускаем все подряд идущие скобки одного типа
                    while (i < s.length() && s.charAt(i) == currentChar) {
                        i++;
                    }
                }

                if (!smileyDetected) {
                    result.append(":-");
                }
            } else {
                result.append(s.charAt(i));
                i++;
            }
        }

        return result.toString();
    }
```

``` java

    public static String test(String s) {
        StringBuffer stringBuffer = new StringBuffer();

        for (int i = 0; i < s.length(); i++) {

            if (s.startsWith(":-", i)) {

                while (s.startsWith(":-", i + 2)) {
                    stringBuffer.append(s, i, i + 2);
                    i += 2;
                }
                i += 2;
                if(i >= s.length()) {
                    stringBuffer.append(":-") ;
                    break;
                }

                char a = s.charAt(i);
                if (a == '(' || a == ')') {
                    while (i < s.length() && s.charAt(i) == a) {
                        i++;
                    }
                } else {
                    stringBuffer.append(":-") ;
                }
            }
            if(i >= s.length())break;
            if(s.charAt(i) == ':'){
                i-=1;
                continue;
            }
            stringBuffer.append(s.charAt(i));
        }
        return String.valueOf(stringBuffer);
    }
}
```