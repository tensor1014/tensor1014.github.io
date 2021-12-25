iterator

- 作用：不知道类的实现细节也能够遍历其数据
- 接口定义
  ```java
  public interface Iterable<T> {
    Iterator<T> iterator();
  }
  public interface Iterator<E> {
    boolean hasNext();
    E next();
    void remove();
  }
  ```
- 实现了 Iterable 的类可以在实现多个 Iterator 内部类，MutilIterator 实现了三种迭代器，分别是默认的前向迭代器，反向迭代器和随机迭代器。主函数中分别调用了三种迭代器进行遍历。

  ```java
  public class MutilIterator implements Iterable<String> {
  private String[] words = "May I get offers this summer.".split(" ");

      //默认的迭代器，前向遍历
      public Iterator<String> iterator() {
        //匿名内部类
          return new Iterator<String>() {
              private int index = 0;
              public boolean hasNext() {
                  return index < words.length;
              }
              public String next() {
                  return words[index++];
              }
              public void remove() { // Not implemented
                  throw new UnsupportedOperationException();
              }
          };
      }

  //反向迭代器
      public Iterable<String> reverseIterator() {
          return new Iterable<String>() {
              @Override
              public Iterator<String> iterator() {
                  return new Iterator<String>() {
                      private int index = words.length - 1;
                      public boolean hasNext() {
                          return index > -1;
                      }
                      public String next() {
                          return words[index--];
                      }
                      public void remove() { // Not implemented
                          throw new UnsupportedOperationException();
                      }
                  };
              }
          };
      }
  ```
