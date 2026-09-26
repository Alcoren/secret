# secret
```
int change_left(int num) {
    int sign = 1;
    if (num < 0) {
        sign = -1;
        num = -num;
    }
    if (num == 0) return 0;

    // Считаем, сколько цифр в числе
    int digits = 0;
    int temp = num;
    while (temp > 0) {
        digits++;
        temp /= 10;
    }

    // Если цифр нечётное количество — самая правая остаётся без пары
    int last = -1;
    if (digits % 2 == 1) {
        last = num % 10;
        num /= 10;
        digits--;
    }

    // power — это 10^(digits-2), т.е. разряд первой пары слева
    int power = 1;
    for (int i = 0; i < digits - 2; i++) {
        power *= 10;
    }

    int ans = 0;
    while (power > 0) {
        int pair = num / power;                     // первые две цифры
        int swapped = (pair % 10) * 10 + pair / 10; // меняем их местами

        ans = ans * 100 + swapped;                  // приклеиваем справа
        num = num % power;                          // убираем обработанные цифры
        power /= 100;
    }

    if (last >= 0) {
        ans = ans * 10 + last;                      // непарная правая цифра
    }

    return sign * ans;
}
```



```
int change_left_skip(int num) {
    int sign = 1;
    if (num < 0) {
        sign = -1;
        num = -num;
    }
    if (num == 0) return 0;

    int digits = 0;
    int temp = num;
    while (temp > 0) {
        digits++;
        temp /= 10;
    }

    int last = -1;
    if (digits % 2 == 1) {
        last = num % 10;
        num /= 10;
        digits--;
    }

    int power = 1;
    for (int i = 0; i < digits - 2; i++) {
        power *= 10;
    }

    int ans = 0;
    int pairIndex = 0;         // номер пары: 0, 1, 2, 3, ...
    while (power > 0) {
        int pair = num / power;
        int result;

        if (pairIndex % 2 == 0) {
            // чётная пара (0, 2, 4...) — переворачиваем
            result = (pair % 10) * 10 + pair / 10;
        } else {
            // нечётная пара (1, 3, 5...) — оставляем как есть
            result = pair;
        }

        ans = ans * 100 + result;
        num = num % power;
        power /= 100;
        pairIndex++;
    }

    if (last >= 0) {
        ans = ans * 10 + last;
    }

    return sign * ans;
}
```
