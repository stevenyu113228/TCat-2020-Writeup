# T-Cat 2020 Writeup
## T貓盃 2020



## [第1題]  破解密碼(弱密碼)
想要成為一個及格的程式設計師或是合格的駭客，突破帳號密碼的限制是最基本的能力，這裡有一個工業控制系統的登入頁面，你能成功登入取得重要資訊嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20001/

附件下載:無附件

### 解法
- 帳號`admin`
- 密碼`admin`

---
## [第2題]  破解密碼(SQL Injection)
繞過帳號密碼的方式可不只一種，雖然看似是一個普通的網頁，和其他頁面長的沒什麼不一樣，立面卻暗藏著豐厚的學問，這是一個工業控制系統的登入頁面，你能成功登入取得重要資訊嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20002/ 

附件下載:無附件

### 解法
- 帳號:`admin`
- 密碼:`or '1'='1`

## [第3題]  破解密碼(SQL Injection)
這次程式設計師不會再犯低級的錯誤了，這次資料庫針對密碼的欄位有做適當的編碼，你還能成功登入這個控制系統取得重要資訊嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20003/ 

### 解法
- 帳號:`1' or 1=1 -- -`
- 密碼:`meow`

## [第4題]  權限漏洞(權限弱點)
在某個工控系統中，已知可以使用帳號:nckuuser 與 密碼: nckuuser 進行登入，但是若想要取得Flag需要取得管理者權限，你有辦法取得管理者權限嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20004/ 

附件下載:無附件

### 解法
登入之後觀察cookie有一項為`nckuuser`，把它改為`admin`

## [第5題]  程式弱點(程式碼漏洞)
Modbus是一種序列通訊協定，是工業電子裝置之間常用的連接方式，也是工業領域通信協定的業界標準。 某天有人在這個查詢網站上發現了index的備份檔並且寄給你，如附件，你能想想辦法繞過程式的限制，查詢到重要的資訊嗎? 

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20005/ 
```php
<?php
 error_reporting(E_ALL^E_NOTICE^E_WARNING);
 $search = isset($_GET['user_search']) ? $_GET['user_search'] : 'searchContent';
 if($search === searchContent)
 {

 }
 else if(strpos($_SERVER['QUERY_STRING'],'user_search') !==false)
 {
  echo "<p>查詢指令不正確</p>" ;
 }
 else if($search < 1000)
 {
  echo "<p>查詢指令長度太短了</p>";
 }
 else if((string)$search > 0)
 {
  echo "<p>查詢指令長度太長了</p>";
 }
 else
 {
  echo "<p>查詢結果</p>";
  echo "<p>{\"TCat2020\":\"???????????????????????????\"}</p>";
 }
?>
```

### 解法
這一題比賽時我沒有解出來，不過聽大神的講法是可以用空白鍵來繞過


## [第6題]  加密漏洞(RSA)
RSA是當代密碼學非常重要的技術之一，從金鑰交換到憑證簽名都可以看的到RSA的影子，但由於RSA在加密和解密上複雜度較高，所以在大部分的工業控制系統上較少見RSA加密技術，或是改使用較短的金鑰進行加解密，也因為如此造成工業控制系統上雖然有使用到RSA加密技術，卻很容易被破解。目前在這個系統上，有取得加密後的文件代碼為7217220且已知公鑰為 (e,N) = (252323,13886599) 你能幫我找出原始的代碼是多少嗎? 

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20006/ (https://es.tcat2020.twisc.ncku.edu.tw:20006/) 

### 解法
直接寫Py暴力破解答案出來
```python
e = 252323
N = 13886599
c = 7217220
for i in range(2**24):
    n = i
    if pow(n,e,N) == c:
        print(n)
```

## [第7題]  編碼與識別(編碼與OCR)
天啊! 我的檔案好像被莫名的程式給加密了，裡面可是藏著非常非常重要的管理代碼，誰快來幫我把他解開，解開後你就能夠成功找到管理系統的代碼，我不會讓你失望的!! 

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20007/ 

附件下載: https://es.tcat2020.twisc.ncku.edu.tw:20007/file/password.crypto

### 解法
題目給的是一個用base64編碼後的圖片，解開後會看到這個樣子的語言
![](https://i.imgur.com/8GaUj7n.png)
用Google翻譯後得知是"印地語"
意思是`Cat{You can't type these}`
用OCR軟體取出文字後，貼上即可


## [第8題]  數位憑證(數位憑證)
SSL憑證一個是數位證書，用來驗證網站的身分並且可以使用SSL技術將資料加密，也就是說，SSL可以用於保護網際網路連線安全以及防止兩個終端之間發送的敏感資料被駭客竊聽或修改。 而這個網站同樣也受到SSL的保護，你能幫我查詢比賽的網址es.tcat2020.twisc.ncku.edu.tw的憑證指紋是多少嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20008/

附件下載:無附件

### 解法
用瀏覽器就可以看出SSL憑證指紋的hash
但是提交後都失敗，懷疑是格式的問題
另外我也把憑證載下來跑
```
openssl x509 -noout -fingerprint -sha256 -inform pem -in [certificate-file.crt] 
 
openssl x509 -noout -fingerprint -sha1 -inform pem -in [certificate-file.crt]
 
openssl x509 -noout -fingerprint -md5 -inform pem -in [certificate-file.crt] 
```
但是題目都不吃
我覺得應該要說明清楚需要的格式
例如使用冒號、減號、空白分隔，或是不分隔等方式

## [第9題]  IP 弱點(偽造IP)

在工業控制的環境下，為了保護各設備間的通訊安全，絕大部分的工業控制系統被限定只有在內網才可以訪問，藉此避免被外部設備惡意掃描或攻擊，已知此網站的"PLC管理"是需要在內網中才可以訪問的，你能幫我繞過這個限制，取得重要的資訊嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20009/

附件下載:無附件

### 解法
這一題我也沒有解出來。
網頁進入後會要求說需要使用`192.168.10.251`進入管理頁面
我透過改Header的方法
- X-Forwared-For
- X-Originating-IP
- X-Remote-IP
- X-Remote-Addr
- 都失敗

## [第10題]  檔案編碼驗證(檔案編碼驗證)

朋友傳給我一個很重要的檔案在附件中，說裡面藏有重要的資訊，只要一被竄改，可能就會導致嚴重的後果，但我無法確認他傳來的檔案是否是正確的，你能想個辦法幫我驗證這個檔案有沒有被竄改過嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20010/

附件下載:下載

### 解法
就...把檔案丟去sha256還是sha1我忘了QQ。然後把hash值填上去就好ㄌ

## [第11題]  ZIP 解密(ZIP 解密)

好久以前我怕我會忘記網站登入的帳號密碼，因此把一份儲存網站帳號密碼的檔案壓縮在這個壓縮檔裡面並且有加密，但我現在反而忘記解壓縮密碼了，要是不能解開的話就糟糕了，恐怕再也進不了這個系統，你能幫我解開它嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20011/

### 解法
目測裡面只有一個Password.zip，感覺起來只能用暴力破解的方法，測了1000個弱密碼失敗，我就懶得解ㄌㄏㄏ。

## [第12題]  中繼憑證解析(中繼憑證解析)

SSL憑證具有階層式的關係，是一層一層簽發下來的，而這個網站的憑證也具有類似的結構，你能幫我查詢比賽的網址https://es.tcat2020.twisc.ncku.edu.tw的中繼憑證指紋是多少嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20012/

附件下載:無附件


### 解法
同第8題，不知道他希望ㄉ答案是什麼。


## [第13題]  封包解析(封包解析)

HTTP是由Tim Berners-Lee於1989年在歐洲核子研究組織（CERN）所發起，是一個客戶端和伺服器端之間請求和應答的標準，不過HTTP是一個非加密的協定，並不安全，目前我們已經透過網管型的交換器錄到一段使用者的封包，你能從中幫我解析出登入的資訊嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20013/

附件下載:下載

### 解法
提供了一個鯊魚檔案，用鯊魚打開會看到20個封包。
裡面就有Flagㄌ
![](https://i.imgur.com/0nVz989.jpg)

## [第14題]  圖片影藏(圖片影藏)

《蒙娜麗莎》是由文藝復興時期的著名畫家Leonardo da Vinci所畫的肖像畫，目前保存在巴黎的羅浮宮中，而《蒙娜麗莎》這幅畫傳聞藏著許多的秘密，這次給你的這幅畫也不例外，你能找出這張《蒙娜麗莎》所隱藏的資訊嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20014/

附件下載:下載

### 解法
用Binwalk可以看到一個zip藏在圖片裡面，然後用foremost拆開就會取得一個有flag的zip檔案。
![](https://i.imgur.com/faRnAJl.png)


## [第15題]  PHP字串缺陷(PHP字串缺陷)

某天你在這個網站上發現了index的備份檔，如附件，裡面似乎藏著很重要的資訊，可以用來逃避帳號密碼的限制，你能找出正確的方法來登入取得重要資料嗎?

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20015/ 

附件下載:下載 https://es.tcat2020.twisc.ncku.edu.tw:20015/index.php.bak
```php
<?php
 error_reporting(E_ALL^E_NOTICE^E_WARNING);
 $account = $_POST['account'];
 $password = $_POST['password'];
 $Sourse = false;
 if(md5($account)==sha1($password))
 {
  $Sourse = true;
 }
 else
 {
  $Sourse = false;
 }
?>
```
### 解法
這一題是考php的0e問題，php在做==時，會把0e開頭的字串當作是科學記號來解，所以就找0e開頭的md5跟0e開頭的sha1值提交。
- 帳號:`QNKCDZO`
- 密碼:`aaroZmOk`



## [第16題]  封包解析(封包解析)

咦?奇怪了，第16題? 我以為只有15題呢….。別擔心，我有可靠的消息告訴我，第16題的答案就藏在前15題中，快來把這道題目給解開吧!!

解題網址:https://es.tcat2020.twisc.ncku.edu.tw:20016/ 

附件下載:無附件

### 解法
通靈題，我看前面題目的封包、原始碼，什麼都看不出來，所以就沒解ㄌQQ



## 心得
- 主辦單位是用自製的解題系統，輪循使用<1秒的ajax,因此導致系統崩潰了很多次，也在中途換了一台Server。

- 原本的考試時間是9:30~11:30，但是11:30後還可以繼續作答，直到12:13主辦單位才發出通知說延長，還修改ㄌ計分方式。

- 如果不改計分方式ㄉ話我的名次應該會更高QQ。

![](https://i.imgur.com/Upzn5xl.jpg)



- 最終獲得ㄌ優勝
![](https://i.imgur.com/pBZs9Ir.jpg)

