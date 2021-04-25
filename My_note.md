#my note

```python
from pwn import *

r = remote('140.110.112.22', 2402)

r.recvuntil('year :')
r.recvuntil('year :')

for i in range(1,101):
	r.recvuntil("year :")
	year = r.recvuntil("\n")
	year = year.decode()
	year = year.strip()
	year = int(year)
	print(year)
	
	if year%4 == 0 and not year%100 == 0:
		r.sendline(b'leap')
	elif year%400 == 0 :
		r.sendline(b'leap')
	else:
		r.sendline(b'ordinary')

r.interactive()
