- `make` 构建的 `map` 返回的是一个引用
- Go 推荐使用简短的明明，尤其是对于小作用域的局部变量。作用域越大，命名越长
- `zero value` 
    | type                                                             | zero value                  |
    |------------------------------------------------------------------|-----------------------------|
    | int                                                              | 0                           |
    | string                                                           | ""                          |
    | bool                                                             | false                       |
    | refernce type (`slice`, `pointer`, `map`, `channel`, `function`) | nil                         |
    | interface                                                        | nil                         |
    | aggregate type (`array`, `struct`)                               | type with zero value fileds |
## 声明 Declaration
`var`, `const`, `type`, `func`
```go
var i, j, k int
var b, f, s = true, 2.3, "string"
var f, err = os.Open(name)
i := 100
i, j := j, i    // swap values of i and j

in, err := os.Open(inFile)
// ..
out, err := os.Open(outFile)    // declare new variable out, assign new value to existing variable err

// Pointer
x := 1
// &x address of x
//  p, of type *int, pointer to x
p := &x     
fmt.Println(*p) // "1"
*p = 2 // equivalent to x = 2
fmt.Println(x) // "2"
```
`new(T)` 创建了一个 `T` 类型的未命名变量, 初始化为 `T` 类型的零值, 返回这个值的地址， 类型 `*T`

```Go
p := new(int)   // p, of type *int, points to an unnamed int varaible
fmt.Println(*p) // "0"
*p = 2
fmt.Println(*p) // "2"
```
Tuple assignment
```Go
v, ok = m[key]  // map lookup
v, ok = x.(T)   // type assertion
v, ok <-ch      // channel receive
n, err = io.Copy(dst, src)
_, ok = x.(T)   // check type but discard result
```
Type Declaration
`type name underlying-type`
Conversion
```go
// type Celsius float32
// type Fahrenheit float32
var c Celsius
var f Fahrenheit
fmt.Println(c == 0) // "true"
fmt.Println(f >= 0) // "true"
fmt.Println(c == Celsius(f)) // "true"
fmt.Println(c == f) // compile error: type mismatch
```
Package initialization
包初始化
    - 按照依赖的顺序，依次加载依赖包
    - 按照文件名顺序读取包文件
    - 按照声明顺序初始化变量
    - 执行初始化函数 `func init()`


