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
> $n$ , $c$ が与えられる. RSA暗号を解読せよ. ただし, $q=2p+1$ である.

$n=pq=2p^2+p$ なので $p$についての二次方程式を解くことで $p$, $q$ を求めることができます.

以下のコードで答えを求めることができます.

```python
from sage.all import var, solve
from output import n, c
from Crypto.Util.number import long_to_bytes

e = 65537

x = var('x')
solutions = solve(2 * x ** 2 + x - n == 0, x)

p = int(max(solutions).rhs())
q = 2 * p + 1
d = pow(e, -1, (p - 1) * (q - 1))

print(long_to_bytes(pow(c, d, n))) # ctf4b{R3l4ted_pr1m3s_4re_vuLner4ble_n0_maTt3r_h0W_l4rGe_p_1s}

```
