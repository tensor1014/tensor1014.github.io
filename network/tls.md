# TLS

**TLS** is short for Transport Layer Security.

## 对称加密算法

`A`和`B`都使用同一个秘钥`key`分别进行加密和解密，并将加密后的数据`dataA`通过网络进行传输。这个时候数据是安全的，但存在一个问题，秘钥`key`怎么传输，如果通过网络传递，密码可能被中间人截获。
对称加密算法有:

- DES
- triple-DES
- AES

```python
# A
dataA = encrypt(data, key)
# B
data = decrypt(dataA, key)
```

## 非对称加密

非对称加密算法有两个秘钥，public key `PubKey`和 private key `privKey`。
公钥加密，私钥解密，`pubKey`加密过的数据可以被`privKey`解密。
私钥签名，公钥验签。

A 和 B 仍要需要相互交换公钥，中间人可以将自己的公钥发送给 AB，截获和篡改数据。

```python
# A
digestA = digest(hash(data), privKeyA)
dataA = encrypt(data, pubKeyB)
# B receive digestA + dataA
data = decrypt(dataA, privKeyB)
hashA = validate(dataA, pubKeyA)
# 校验数据是否完整
if hashA === hash(data) OK
```

## CA

TLS 通过 CA(Certificate Authority)来保证 public key 的真实。
CA 也是基于非对称加密来工作。

### 借助 CA，B 将公钥通过网络完整的传输给 A。

B 将自己的公钥和身份信息传给 CA，CA 使用自己的私钥加密这些数据，生成数字证书。
B 将数字证书通过网络传输给 A。A 收到后，会通过 CA 发布的 CA 证书（包含 CA 的公钥)来验签 B 的数字证书是真实的，从而获取数字证书中 B 的公钥。

A 的浏览器或操作系统中内置了信任的 CA 证书，不必通过网络获取。
中间人没有 CA 的私钥，无法伪造处有效的数字证书。

```python
# B
CSR = pubKeyB + hostB
signB = digest(CSR, privKeyCA)
CRT = CSR + signB
# A
CSR2 = validate(CRT, pubKeyCA)
if (CSR2 === CSR) OK
```

### 信任链

1. B 信任 CA1
2. A 信任 CA2，CA2 的公钥可以验证 CA1，验证通过则 A 信任 CA1
3. A 使用 CA1 公钥验证 B 的 CRT

如果 A 不信任 CA2，可以通过 CA3 来验证 CA2，以此类推，B 的 CSR 就可以通过 CA1，CA2，CA3，...，CA 来实现验证，从而实现一条信任链。

信任链的顶端被成为`root CA`，root CRT 是自己签名的。

```python
CSR = pubKeyRoot + hostRoot
CRT = CSR + digest(CSR, privKeyRoot)
```

## TLS 握手

1. 客户端向服务端发送`Client Hello`消息，这个消息包含了一个用户客户端生成的随机数`Random 1`、客户端支持的加密套件 (`Support Ciphers`)、`SSL Version` 和`Session ID`等信息。
2. 服务端向客户端发送`Server Hello`消息，这个消息会从 Support Ciphers 中确定一份加密套件来决定后续加密和生成摘要使用哪些算法，并且还会生成一份随机数`Random 2`。
3. Certificate 服务端将自己的证书下发给客户端，客户端通过 CA 验证证书身份，并去除证书中的公钥。
4. `Server Key Exchagne`: DH 算法通过这一步发送服务器使用的 DH 参数，RSA 不需要这一步。
5. `Certificate Request`服务端要求客户端上报证书。双向验证，用于安全性要求高的场景， 可选。
6. `Server Hello done`服务端通知客户端 Server Hello 过程结束。
7. 客户端使用服务端的公钥加密`Random 3`生成 `PreMaster Key`。
8. 服务端使用私钥从`PreMaster Key`中解出`Random 3`，两端都根据同样的算法将`Random1 + Random2 + Random3`生成同一份秘钥，握手结束后的应用数据层使用这个密码对数据进行对称加密。
9. `Change Cipher Spec(Client)`客户端通知服务端后续消息都会使用之前协商出来的秘钥加密，`。
10. `Encrypted Handshake Message(Client)` Client Finish 消息，客户端将前面握手消息生摘要用协商好的秘钥进行加密，这是客户端发送出来的第一条加密消息。服务端接收到后会使用秘钥解密，确认秘钥是否一致。
11. `Change Cipher Spec(Server)`通知后续消息都是加密消息。
12. `Encrypted Handshake Message(Server)` Server Finish 消息，服务端将握手信息生成摘要再用秘钥进行加密，这是服务端发出的第一条加密消息。客户端使用秘钥解密，确认秘钥是否一致。

优化：`Client Hello`中会附带之前的`Session ID`，服务端收到这个`Session ID`后能服用之前的密钥，不用再次进行后续的握手过程。

## TLS 步骤

1. A 和 B 通过 CA 体系交换公钥
2. 通过非对称加密算法，交换用户对称加密的秘钥
3. 通过对称加密的算法，加密正常的网络通信
