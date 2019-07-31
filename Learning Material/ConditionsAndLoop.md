#### if, if-else, if-else if

If like in all other languages `if` meant for checking conditions. 

```
public class IfConditionExample {
    public static void main(String s[]) {
        int i = 10;
        int j = 5;
        if(i>j) {
            System.out.println("i is bigger than j");
        } 
    }
}

```

If - else 

The block of code following else is executed when the condition checked by `if` is false.

```
public class IfConditionExample {
    public static void main(String s[]) {
        int i = 10;
        int j = 5;
        if(i>j) {
            System.out.println("i is bigger than j");
        } else {
            System.out.println("i is smaller than j");
        }
    }
}

```
**Activity:** Ask the user for a number input and accept the number input and see if the number is greater than 10

Let's use the 
If-else if - We use this when we have more than two conditions to check. Before we see this example, let's look at another class we will be using in the example to understand if-else if. LocalDateTime is a class which we can use to get the date/time. This class is a part of the util package and is not available by default. We have to import it. 

```
import java.time.LocalDateTime;

//This class prints the date when you run it
public class PrintDateAndTime {
    public static void main(String s[]) {
        LocalDateTime localDateTime = LocalDateTime.now();
        System.out.println(localDateTime.getDayOfMonth() +
                " "+ localDateTime.getMonth()+
                " "+ localDateTime.getYear());
    }
}
```

Let's use the LocalDateTime to print an appropriate statement for eadh day of the week.

```
import java.time.LocalDateTime;
public class IfElseIfConditionExample {
    public static void main(String[] s) {
        LocalDateTime localDateTime = LocalDateTime.now();
        String dayOfWeek = localDateTime.getDayOfWeek().toString();
        if(dayOfWeek.equalsIgnoreCase("Monday")) {
            System.out.println("It is the first day of the week!");
        } else if (dayOfWeek.equalsIgnoreCase("Tuesday")) {
            System.out.println("It is the second day of the week!");
        } else if (dayOfWeek.equalsIgnoreCase("Wednesday")) {
            System.out.println("Mid-week already!");
        } else if (dayOfWeek.equalsIgnoreCase("Thursday")) {
            System.out.println("One more day before you say TGIF");
        } else if (dayOfWeek.equalsIgnoreCase("Friday")) {
            System.out.println("Hurray! The last day of the work week");
        } else if (dayOfWeek.equalsIgnoreCase("Saturday")) {
            System.out.println("Weekend! Blissful!");
        } else if (dayOfWeek.equalsIgnoreCase("Sunday")) {
            System.out.println("Make hay while the Sun(day) shines!");
        }

    }
}

```
**Activity** Use combination of `if` and `logical operators` to print whether the current day is a weekday or weekend. 
