# π‘ μμ μ°ΎκΈ°

&nbsp; μμλ 1κ³Ό μκΈ° μμ μ μ μΈν μμ°μλ‘λ λλμ΄ λ¨μ΄μ§μ§ μλ μμ°μμ΄λ€. λ¨, 1μ΄μμ΄μ¬μΌ νλ€.   
μλ₯Ό λ€μ΄ 1, 2, 3, 6μΌλ‘ λλμ΄ λ¨μ΄μ§λ 6μ μμκ° μλλ€.   
νμ§λ§ 1κ³Ό 7μ μ μΈνκ³ λ λλμ΄ λ¨μ΄μ§μ§ μλ 7μ μμμ΄λ€.   

μμλ₯Ό μ°Ύμ λ μ½μμ μ±μ§μ μ΄μ©νλ©΄ ν¨μ¨μ μΌλ‘ κ΅¬νν  μ μλ€.  
- μ½μμ μ±μ§  
  : λͺ¨λ  μ½μμ λνμ¬ κ°μ΄λ° μ½μλ₯Ό κΈ°μ€μΌλ‘ νμ¬ λμΉ­μ μ΄λ£¬λ€.

    <img src="https://user-images.githubusercontent.com/70243735/121998916-9243fa00-cde7-11eb-8cde-73edcc8a535f.png" width ="300px">

<br>

## π‘ μμ νλ³ ν¨μ μ½λ

```python
import math

def is_prime_number(x):
    # 2λΆν° xμ μ κ³±κ·ΌκΉμ§μ λͺ¨λ  μλ₯Ό νμΈνμ¬
    for i in range(2, int(math.sqrt(x))+1):
        # xκ° ν΄λΉ μλ‘ λλμ΄ λ¨μ΄μ§λ€λ©΄ μμκ° μλ
        if x % i == 0:
            return False
    return True
print(is_prime_number(7))
print(is_prime_number(12))
```

<br>

## π‘ μλΌν μ€νλ€μ€μ μ²΄

&nbsp; νλμ μκ° μλ, μ¬λ¬κ°μ μκ° μμμΈμ§ μλμ§λ₯Ό νλ³ν λ μ¬μ©νλ λνμ μΈ μκ³ λ¦¬μ¦μ΄λ€.
μλΌν μ€νλ€μ€μ μ²΄λ Nλ³΄λ€ μκ±°λ κ°μ λͺ¨λ  μμλ₯Ό μ°Ύμ λ μ¬μ©ν  μ μλ€.

**[ λμ λ°©μ ]**
1. 2λΆν° NκΉμ§μ λͺ¨λ  μμ°μλ₯Ό λμ΄νλ€.
2. λ¨μ μ μ€μμ μμ§ μ²λ¦¬νμ§ μμ κ°μ₯ μμ μ iλ₯Ό μ°Ύλλ€.
3. λ¨μ μ μ€μμ **iμ λ°°μλ₯Ό λͺ¨λ μ κ±°**νλ€.  
    : iλ μ κ±°νμ§ μλλ€. iλ μμμ΄λ€.
4. λμ΄μ λ°λ³΅ν  μ μμλκΉμ§ 2~3λ² κ³Όμ μ λ°λ³΅νλ€.

<br>

<img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif">


<br>
<br>

## π‘ μλΌν μ€νλ€μ€μ μ²΄ κ΅¬ν μ½λ

μλΌν μ€νλ€μ€μ μ²΄λ₯Ό μ΄μ©νμ¬ 2λΆν° 100κΉμ§ λͺ¨λ  μμ λνμ¬ μμλ₯Ό μ°Ύλ μ½λμ΄λ€.

```python
import math

n = 100
numbers = [True for i in range(n+1)]

# 2λΆν° nμ μ κ³±κ·ΌκΉμ§ λͺ¨λ  μλ₯Ό νμΈ
for i in range(2, int(math.sqrt(n))+1):
    # λ¨μ μ μ€μμ(= μμ μ€μμ)
    if numbers[i]:
        # iλ₯Ό μ μΈν iμ λͺ¨λ  λ°°μ μ­μ 
        j = 2
        while i * j <= n:
            numbers[i * j] = False
            j += 1

# λͺ¨λ  μμ μΆλ ₯
for i in range(2, n+1):
    if numbers[i]:
        print(i, end=' ')
```