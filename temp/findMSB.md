```
int findMSB(int n)
{
    n |= n >> 1;	// MSB로부터 다음 2칸은 1이 된다.
    n |= n >> 2;	// MSB로부터 다음 4칸은 1이 된다.
    n |= n >> 4;	// MSB로부터 다음 8칸은 1이 된다.
    n |= n >> 8;	// MSB로부터 다음 16칸은 1이 된다.
    n |= n >> 16;	// MSB로부터 다음 32칸은 1이 된다.
	
    n = n + 1;	// MSB 바로 앞 자리만 1이 된다.
	
    return (n >> 1);	// MSB만 1로 변환하여 리턴한다.
}
```
32bit int 값을 1,2,4,8,16칸 쉬프트해가면서 최상위 bit 이하를 1로 채웠다가  
최상위비트값만 뽑아주기 위해 1을 더해주고 다시 쉬프트 1번  
  
* n은 2의30승-1 이하여야 한다.  

* MSB가 31번째 자리인 경우 마지막에 right shift할때 오류  
01111111111111111111111111111111  
10000000000000000000000000000000  
11000000000000000000000000000000  
  
* MSB가 32번째 자리인 경우 1을 더할때 오버플로우  
11111111111111111111111111111111  
00000000000000000000000000000000  
00000000000000000000000000000000  


이걸 피하는 방법은 없을까?
```
int findMSB(unsigned int n)
{
    n |= n >> 1;	// MSB로부터 다음 2칸은 1이 된다.
    n |= n >> 2;	// MSB로부터 다음 4칸은 1이 된다.
    n |= n >> 4;	// MSB로부터 다음 8칸은 1이 된다.
    n |= n >> 8;	// MSB로부터 다음 16칸은 1이 된다.
    n |= n >> 16;	// MSB로부터 다음 32칸은 1이 된다.
	
	n = ((n + 1) >> 1) |
		(n & (1 << ((sizeof(n) * 8) - 1)));
	return n;
}
```
input이 unsigned int임에 주의
32번째 bit를 확인해서 살려주는 방식