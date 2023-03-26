# 정수값의 절대값 구하기  

```
#include <stdio.h>

void printDigits(int v)
{
	int n = sizeof(v) * 8;
	for (int i = n - 1; i >= 0; i--)
	{
		printf("%d", v & (1 << i) ? 1 : 0);
	}
	printf("\n");
}

unsigned int getAbsoluteValue(int v)
{
	//printDigits(v);
	int const mask = v >> sizeof(int) * 8 - 1;
	//printDigits(mask);
	//printDigits(v + mask);
	//printDigits((v + mask) ^ mask);
	return (v + mask) ^ mask;
	//return (v ^ mask) - mask;
}

int main(void)
{
	int v = -9999;
	getAbsoluteValue(v);
}
```

부호를 표현하는 2진수에서 부호를 바꾸려면 2의 보수를 구하면 된다.  
비트를 반전시킨 후 (1의 보수) 1을 더한 값  
<B>이를 거꾸로 생각하면 1을 빼준 후 반전시킨 값</B>  

v가 음수인 경우  
1을 빼준 후 비트를 반전시키면 절대값이 나온다.  
v의 size-1 만큼 left shift한 값은 111...11₂ = -1  
v의 절대값은 v에 위의 mask를 더해서 v와 xor한 값  (1을 뺀 값의 1의 보수)  
혹은 v에 mask를 xor하고 나온 v의 1의 보수 값에 1을 더한 값  
```
r = (v + (-1)) ^ (-1)  
r = (v ^ (-1)) - (-1)
```

v가 양수인 경우  
v의 size-1 만큼 left shift한 값은 000...00₂  = 0  
v의 절대값은 v에 mask를 더해서 v와 xor한 값 (v ^ 0)  
혹은 v에 mask를 xor하고 나온 v에 0을 뺀 값 (v - 0)  
```
r = (v + 0) ^ 0  
r = (v ^ 0) - 0
```
  
  
