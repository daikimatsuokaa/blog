+++
title = 'SECCON Beginners 2024 (crypto)'
date = 2024-06-30T21:47:24+09:00
draft = false
tags = ["CTF", "Cryptography"]
+++

SECCON Beginners CTF 2024のcrypto分野のwriteupです.

Beginner 向けということで, 最初の問題は取り組みやすく, かつ後半の問題は歯応えのある, とても良いセットでした. 

## Safe Prime (362 team solved)

> **問題** 
>
> RSA暗号を使用して暗号化されたメッセージ $c$ を復号せよ.
> 以下の情報が与えられている. 
> - 公開鍵 $n  (=pq)$ と $e$ の値.
> - $p>q$ とすると, $q=2p+1$ が成り立つ.

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

> **答え**
>
> ctf4b{R3l4ted_pr1m3s_4re_vuLner4ble_n0_maTt3r_h0W_l4rGe_p_1s}

## math (119 team solved) 

> **問題**
>
> RSA暗号を使用して暗号化されたメッセージ $c$ を復号せよ.
> 以下の情報が与えられている.
> - 公開鍵 $n (=pq)$ と $e$ の値.
> - $a=p-x$ , $b=q-x$ として, その積 $ab$ の値. ( $a, b, x$ の値はわからない)
> - $a$ の約数 $a'$ , $b$ の約数 $b'$ の値.
> - $a, b, x$ は平方数.
