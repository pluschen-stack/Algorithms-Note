# 素性测试

$$
费马小定理：如果p是一个素数，那么对于任意的1\le a \lt p ，有a^{p-1} \equiv 1 \pmod p
$$

因此可以设计算法进行素性测试，如下：

```c
function primality(N):
Input:Positive integer N
Output: yes/no

Pick a positive integer a < N at random
if pow(a,N-1) = 1 (mod N):
    return yes
else:
    return no
```

但是存在一些合数它们对于一些a的取值也可以通过上述的算法。不过根据书上的看法，如果a与N不互质的话，应该是不会通过费马测试的。所以只考虑与N互素的a就好了。

典型的比如Carmichael数，对于所有与N互素的a，N将通过费马测试。不过幸好对于不是Carmichael数的合数，如果存在a与它互素，这些a的数量至少有一半使得N不能通过费马测试。

$$
引理：如果对于某些与N互素的a，有a^{N-1} \not \equiv 1 \pmod N,\\那么对于a<N的至少一半 的可能取值，N将无法通过费马测试
$$

根据这个引理，当忽略Carmichael数的时候，有如下结论:

$$
P(当N为素数，图1-7中的算法返回yes)=1\\
P(当N不是素数，图1-7中的算法返回yes)\le 1/2
$$

 因此可以写出下面的算法：

```c
function primality(N):
Input:Positive integer N
Output: yes/no

Pick a positive integer a1,a2,a3,...,ak < N at random
if pow(ai,N-1) = 1 (mod N) for all i = 1,2,...,k:
    return yes
else:
    return no
```

对于上面这个算法，再不考虑N是Carmichael数时，他的出错概率很小。

Lagrange定理：

$$
令\pi(x)为\le x的素数的个数，则有\\
\lim_{x\to \infty} \frac {\pi(x)} {x/ lnx}
$$

根据上面这个定理可知，如果有n位二进制数，那么从中去一个数，它是素数的概率约等于1/n。因此，想要随机生成一个素数，可以这样做，随机生成一个二进制数，用上面的素性测试去判断这个二进制数是否是素数，如果是的话，则生成成功，否则继续生成。因为素数的概率约等于1/n，因此只需O\(n\)次即可。

扩展：

（1）为了解决Carmichael数，可以参考Rabin和Miller的素性检测

（2）需要证明对于不与N互素的数a，不能通过费马测试

