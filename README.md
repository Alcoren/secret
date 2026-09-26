# secret
```
#include <stdio.h>

int bitwise_add(int num, int addend);
int rev(int normal);

int main(void){
	int ans = 0;
	int n, m;
	int input

	printf("Введите n и m:\n");
	scanf("%d%d",&n, &m);
	// printf("121344324");
	// scanf("%d", m);
	ans = bitwise_add(n, m);
	printf("\nответ: %d\n", ans);

	return 0;
}

int rev(int normal){
	int inv_num = 0;
	while(normal){
		inv_num = inv_num * 10 + normal% 10;
		normal /= 10;
	}
	return inv_num;
}

int bitwise_add(int num, int addend){
	int ans = 0;
	int y = 0;
	int sign = 1;

	if(num < 0){
		sign = -1;
		num = -num;
	}

	while( num != 0 ){
		y = num % 10 + addend;

		if( y < 0 ){
			y = -y;
		}

		y %= 10;
		ans = ans * 10 + y;
		num /= 10;
	}
	
	ans = rev(ans);

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
