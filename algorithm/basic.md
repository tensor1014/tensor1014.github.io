常见函数:

- 向下取整 $\lfloor x \rfloor$
- 向上取整 $\lceil x \rceil$
- 自然对数 $\ln N = \log_{e} N$
- 以 2 为底的对数 $\lg N = \log_2 N$
- 调和级数 $H_n$
  $$H_n=1+\frac{1}{2}+\frac{1}{3}+...+\frac{1}{n}=\sum_{i=1}^{n}\frac{1}{i}$$
  $$\sum_{i=2}^{n}\frac{1}{i}\lt \int_{0}^{n}\frac{1}{x}\mathrm{d}x=\ln n$$
  $$\sum_{i=1}^{n}\frac{1}{i}\lt \ln n + 1 = O(\log n)$$
- 阶乘 $N! = N \times (N - 1) \times ... \times 2 \times 1$

近似函数:

- 调和级数求和
  $$H_N = 1 + \frac{1}{2} + \frac{1}{3} + ... + \frac{1}{N} \approx ln N$$
- 等差数列求和
  $$等差数列求和 \quad \sum_{i=0}^{n}{a_1 + (i-1) \times d} = na_1 + \frac{n(n-1)}{2} $$
	$$常数数列求和 \quad \sum\_{i=1}^{N}{i} = \frac{N \times (N-1)}{2} \approx N^2/2$$
- 等比数列求和
  $$等比数列求和 \quad \sum_{i=1}^{i=n}{a_1 \cdot q^(i-1)} = \frac{a1(1-q^n)}{1-q} (q \neq 1)$$
  $$2的指数求和 \quad \sum_{i=0}^{n}{2^i} = 1 + 2 + 4 + 8 + ...+ 2^n = 2^{n+1} - 1 \approx 2^{n+1}$$
  $$斯特林公式 \lg n! = \sum_{i=1}^{n}{i} = \lg 1 + \lg2 + ... + \lg n \approx n \cdot \lg n$$
