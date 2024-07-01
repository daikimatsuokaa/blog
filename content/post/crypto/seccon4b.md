+++
title = 'SECCON Beginners 2024 (crypto)'
date = 2024-06-30T21:47:24+09:00
draft = false
tags = ["CTF", "Cryptography"]
+++

SECCON Beginners CTF 2024のcrypto分野のwriteupです.

## Safe Prime (362 Solved)

> **問題** 
>
> RSA暗号を使用して暗号化されたメッセージ $c$ を暗号化せよ. 以下の情報が与えられている. 
> - 公開鍵 $n  (=pq)$ と $e$
> - $p>q$ とすると, $q=2p+1$

$n=pq=2p^2+p$ なので,  $p$ についての二次方程式を解くことで $p$, $q$ を求めることができます.

```python
from output import n, c, e
from sage.all import var, solve
from Crypto.Util.number import long_to_bytes

x = var('x')
solutions = solve(2 * x ** 2 + x - n == 0, x)

p = int(max(solutions).rhs())
q = 2 * p + 1
d = pow(e, -1, (p - 1) * (q - 1))

print(long_to_bytes(pow(c, d, n)))

```
