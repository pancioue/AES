進階加密標準（英語：Advanced Encryption Standard，縮寫：AES）
===============
* 對稱密鑰加密
* 分組密碼

對稱加密:加解密同一把金鑰  
速度  => 對稱 較 非對稱 __優__  
安全性=> 對稱 較 非對稱 __差__ 

加密行為
-----------
將明文 (plan text）二進位資料，分為一塊一塊(block) ，每塊長度跟加密金鑰長度相同(128 / 192 / 256 bit .. )稱為 明文區塊

並透過 AES 演算法，將每一塊明文區塊加密成密文區塊

金鑰長度:
 * AES-128 = 16 bytes  
  字串 長度16  
  HEX 長度 32 (0-9 A-F)  
 * AES-192 = 24 bytes  
  字串 長度24  
  HEX 長度 48 (0-9 A-F)  
 * AES-256 = 32 bytes  
  字串 長度32  
  HEX 長度 64 (0-9 A-F)

引用參考: https://ithelp.ithome.com.tw/articles/10249488


加密模式
---------
有多種加密模式，不需要深入研究  
並非所有模式都需要iv值
* ECB:不需要iv偏移量


填充模式(Padding)
-----------
參考: https://ithelp.ithome.com.tw/articles/10250386  

```
// php code
openssl_encrypt($data, 'AES-256-CBC', $key, OPENSSL_RAW_DATA, $iv); 
```
第四個參數可填 
1. 0
2. OPENSSL_RAW_DATA 
3. OPENSSL_ZERO_PADDING  
4. OPENSSL_RAW_DATA | OPENSSL_ZERO_PADDING
* > OPENSSL_RAW_DATA just tells openssl_encrypt() to return the cipherText as ... raw data.   
    By default, it returns it Base64-encoded.

  引用參考: https://stackoverflow.com/questions/43885574/what-does-openssl-raw-data-do
* OPENSSL_RAW_DATA 與 OPENSSL_ZERO_PADDING 兩者沒有關係
* openssl_encrypt預設就是以 PKCS#7 填充模式，所以只要沒有加 OPENSSL_ZERO_PADDING 參數就是以 PKCS#7 填充
* 這篇 https://stackoverflow.com/questions/68244407/how-to-use-openssl-zero-padding-in-php 
  下面某個回復提到，OPENSSL_NO_PADDING 是 for 非對稱加密，若是如此，OPENSSL_NO_PADDING就不是給 AES-256-CBC 使用的參數，符合官方文件所提的 
  > options is a bitwise disjunction of the flags OPENSSL_RAW_DATA and OPENSSL_ZERO_PADDING.
