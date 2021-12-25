- `Array` 不可变容量, `ArrayList<T>` 可动态扩容
- 声明数组
  ```java
  int[] anArray = new int[10];
  double[] a;
  a = new double[N];
  for (int i = 0; i < N; i++) {
    a[i] = 0.0;
  }
  int[] b = { 1, 2, 3, 4 };
  ```
- cast array to array list
  ```java
  List<String> words = new ArrayList<>(
    Arrays.asList("some words goes here".split(" "))
  );
  ```
- generic array
  ```java
  a = (E[]) new Object[cap];
  ```
