
### Decimal to binary
  
다양한 접근식  

```code
bin(code)[2:]
int(bin(code)[2:])


>>>>> reversed
bin(code)[:1:-1]
```

```
"{0:b}".format(code)

>>>>> reversed
"{0:b}".format(code)[::-1]
```

```
def convertToBinary(n):
   # Function to print binary number for the input decimal using recursion
   if n > 1:
       convertToBinary(n//2)
   print(n % 2,end = '')

# decimal number
dec = 34

convertToBinary(dec)
```

```
# numpy 를 사용하는 방식

from numpy import binary_repr
```
