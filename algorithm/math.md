### 判定一个数是否素数

```java
class math
{
  public static boolean isPrime(int n)
  {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++)
      if (n % i == 0) return false;
    return true;
  }
}
```

### 牛顿迭代法求平方根

![牛顿迭代法示意图](../attachments/NewtonIteration_Ani.gif)

```java
class Math
{
	public static double sqrt(double c)
  {
    if (c < 0) return Double.NaN;
    double err = 1e-15;
    double t = c;
    while (Math.abs(t * t - c) > err)
      t = (c/t + t) / 2.0;
    return t;
  }
}
```

### 最大公约数 Greatest Common Divisor (GCD)

```Go
func gcd(x, y int) int {
  for y != 0 {
    x, y = y, x%y
  }
  return x
}
```

### 佩波那契数列 Fibonacci sequence
每一个元素是前两个元素之和 $0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...$
```Go
func fib(n int) int {
  x, y := 0, 1
  for i := 0; i < n; i++ {
    x, y = y, x+y
  }
  return x
}
```
