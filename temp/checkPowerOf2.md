# 주어진 정수가 2의 제곱수인지 확인하기

```
unsigned int v;
bool f;
f = (v & (v-1)) == 0;
```

2의 n승을 2진수로 표현하면, (n+1)자리만 1이고 나머지는 0이다.
```
2의 0승 = 1 = 0001  
2의 1승 = 2 = 0010  
2의 2승 = 4 = 0100  
2의 3승 = 8 = 1000  
```

2의 n승에서 1을 빼면 n~0 자리까지 1인 숫자가 된다.
이 둘을 AND연산 하면 0이 된다.

|n|2ⁿ|2ⁿ-1|2ⁿ & 2ⁿ-1|
|------|---|---|---|
|0|0001|0000|0000|
|1|0010|0001|0000|
|2|0100|0011|0000|
|3|1000|0111|0000|


위의 코드에서 v가 0인 경우 v-1 이 111...11₂이 되고, f가 0이 되어 2의 제곱수인 것처럼 나온다.
이를 피하려면 아래를 사용해야 한다.
```
unsigned int v;
bool f;
f = v && !(v & (v - 1));
```

v가 0인 경우
```
v & (v-1) = 0
f = 0 && !(0) = 0 && 1 = 0 (false)
```

v가 0이 아니고 2의 제곱수가 아닌 경우
```
v & (v-1) = 0이 아닌 수
f = v && !(0이 아닌 수) = v && 0 = 0 (false)
```

v가 0이 아닌 2의 제곱수인 경우
```
v의 최소값은 2의 0승인 1
v & (v-1) = 0
f = v && !(0) = v && 1 = 1 (true)
```



