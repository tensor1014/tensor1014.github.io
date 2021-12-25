- basic types
  | 类型    | 内存 ( byte) |
  |---------|--------------|
  | boolean | 1            |
  | byte    | 1            |
  | char    | 2            |
  | int     | 4            |
  | float   | 4            |
  | long    | 8            |
  | double  | 8            |
- 对象的内存
  - 对象本身的内存开销 一般是 16 byte
  - 一般内存的使用都会填充为 8 byte （ 64位系统的机器字 )
  - Integer: 24 byte = 对象开销 ( 16 byte ) + int值 ( 4 byte ) + 填充字节 ( 4 byte)
  - Array: 24 byte + ElementSize * N , 24 byte = 对象开销 ( 16 byte ) + 长度 ( 4 byte ) + 填充字节 ( 4 byte )
  - String 64 byte + 2N =  对象开销 (40 byte) + 字符数组 (24 byte + 2 * N)  
    40 byte = 对象开销 ( 16 byte ) + 引用地址 ( 8 byte ) + 字符偏移量 int ( 4 byte ) + 字符串长度 int ( 4 byte) + 哈希 int ( 4 byte ) + 填充字符 ( 4 byte )

- `String`
  - ```java
    String s = "abcde fg";
    s = s.replace(" ", "");
    for (int i = 0; i < s.length(); i++) {
    	char c = s.charAt(i);
    	if (String.valueOf(c).equals('a')) {
    		System.out.println(c, i);
    	}
    }
    ```
