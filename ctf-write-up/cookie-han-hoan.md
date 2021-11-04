---
description: >-
  Write-up về những bài mình giải ra của bên giải a Hazy tổ chức 😂 Định dạng
  flag: Flag{...}
---

# Cookie Hân Hoan

## **Cryptography**

1. **XOR**

![](<../.gitbook/assets/ảnh (26).png>)

{% file src="../.gitbook/assets/encrypt.py" %}

{% file src="../.gitbook/assets/cipher (2).txt" %}

Ở bài này họ sẽ cho ta 1 file encrypt.py và 1 file cipher.txt. Đúng với tên bài, tóm tắt những việc mình sẽ cần làm là tìm ra key và sau đó viết 1 đoạn script để có thể thực hiện tìm flag dựa trên key vừa tìm được.&#x20;

Phép toán XOR tương ứng cú pháp ^ (mọi người có thể tự tìm hiểu thêm về XOR trên google nhé)

Đầu tiên file cipher.txt sẽ cho mình 1 chuỗi hex `6c464b4d514b744817491714487449174b57`

Với định dạng cờ là Flag{}, mình sẽ nghĩ đến với việc XOR thử kí tự F ^ 6c (mục đích tìm ra key), bạn có thể vào link [http://xor.pw/#](http://xor.pw/#) để thực hiện tính nhé.

![](<../.gitbook/assets/ảnh (8) (1).png>)

Như bạn đã thấy thì sau khi XOR F với 6c thì output (key) sẽ là 2a, nếu không chắc chắn, có thể thử tiếp kí tự l với 46, l ^ 46 = 2a. Okay giờ chúng ta đã có key, thực hiện 1 đoạn code dưới đây (ở đây mình dùng C)

```
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
    int key = 0x2a;
    char flag[18]; //khởi tạo mảng flag tối đa 18 kí tự
    int cipher[] = {0x6c,0x46,0x4b,0x4d,0x51,0x4b,0x74,0x48,0x17,0x49,0x17,0x14,0x48,0x74,0x49,0x17,0x4b,0x57};
    for(int i=0;i<18;i++)
    {
        flag[i] = cipher[i] ^ key;
    }
    puts(flag);
}
//Flag{a^b=c=>b^c=a}
```

#### **2. Morse**

![](<../.gitbook/assets/ảnh (30) (1).png>)

{% file src="../.gitbook/assets/morse.wav" %}

Bài này họ sẽ cho mình 1 file .wav để tìm flag, ở đây nhìn tên bài thì cũng đã có đủ hint rồi, mình lười nghe nên đem file lên tool convert luôn :v link mình để đính kèm ở dưới nhé,

Flag{M.O.R.S.E.C.O.D.E}

[https://morsecode.world/international/decoder/audio-decoder-adaptive.html](https://morsecode.world/international/decoder/audio-decoder-adaptive.html)

#### **3. Julius Caesar**

![](<../.gitbook/assets/ảnh (27).png>)

{% file src="../.gitbook/assets/ceasar.txt" %}

Trong file sẽ có 1 đoạn note như sau _Synt{Ry\_Pynfvpb\_Pvcure}. _Nhận thấy đề bài có liên quan tới dạng mật mã Caesar, google tìm tool decode đoạn chữ ra thôi. Ở đây mình dùng [https://www.dcode.fr/caesar-cipher](https://www.dcode.fr/caesar-cipher) để decode

Flag{El\_Clasico\_Cipher}

#### **4. Sixty Four**

![](<../.gitbook/assets/ảnh (15).png>)

Ở bài này, Gà để lại 1 dãy thông điệp như sau `NDY2QzYxNjc3QjVGNUY1RjQyNjE3MzY1MzYzNDc4NDg2NTc4NUY1RjVGN0Q= `có thể thấy đây là 1 chuỗi base64, đem đi decode -> lại thêm 1 chuỗi hex, sau khi decode chuỗi hex to text thì ta sẽ nhận được flag.

Flag{Base64xHex}

> Còn 2 bài cuối là Bruh Aes với Cry More thì mình chưa làm được nên tạm thời chỉ sẽ upload file lên, mọi người có thể giải thử sức nhé.

#### **5. BRUH AES**

![](<../.gitbook/assets/ảnh (17).png>)

{% file src="../.gitbook/assets/aes.py" %}

{% file src="../.gitbook/assets/cipher (1).txt" %}

#### **6. Cry More**

![](<../.gitbook/assets/ảnh (22).png>)

{% file src="../.gitbook/assets/server.py" %}

## Web Basic

1. **Hân Hoan**

![](<../.gitbook/assets/ảnh (21) (1).png>)

Ở thử thách này, họ sẽ cho mình 1 form đăng nhập

![](<../.gitbook/assets/ảnh (29).png>)

Thử đăng nhập bằng username/password bất kì ta sẽ được 1 thông báo như sau

![](<../.gitbook/assets/ảnh (28) (1).png>)

Kiểm tra cookie của trang bằng cách F12, chuyển sang phần Shortage

![](<../.gitbook/assets/ảnh (19) (1).png>)

Ta sẽ thấy lúc này Giá trị (Value) đang là Guest. Và dựa vào thông báo phía trên, ta sẽ thay Guest thành CookieHanHoan và refresh lại trang xem kết quả.

![](<../.gitbook/assets/ảnh (5).png>)

Và thế là xong bài đầu tiên.

Flag{Cookies\_Yummy\_Cookies\_Yammy!}

#### **2. Sause**

![](<../.gitbook/assets/ảnh (2).png>)

Khi vào link đề bài cho thì ta sẽ có 1 form như sau đây

![](<../.gitbook/assets/ảnh (11).png>)

Không có gì đặc biệt hết, nhưng nhìn lại tên đề bài, Sause \~\~ Source? F12 lên xem mã nguồn thôi&#x20;

![](<../.gitbook/assets/ảnh (25) (1).png>)

Và thế là ẵm 1 point tiếp theo về nhà

Flag{Web\_Sause\_Delicious}

#### **3. I Am Not A Robot**

![](<../.gitbook/assets/ảnh (18).png>)

![Giao diện sau khi vào link đề bài](<../.gitbook/assets/ảnh (3).png>)

Đề bài quá rõ ràng rồi, vào luôn /robots.txt kiểm tra thôi

![](<../.gitbook/assets/ảnh (1) (1).png>)



Robots.txt là một tiêu chuẩn mà rất nhiều trang web sử dụng để tương tác với các web crawler và web robots, bằng cách quy định những khu vực nào của trang web cho phép scan. Như ví dụ ở đây, trang web cho phép scan tại **/fl@g1337\_d240c789f29416e11a3084a7b50fade5.txt**, chúng ta xem có gì ở đây nào:

![](<../.gitbook/assets/ảnh (4) (1).png>)

Flag{N0\_B0T\_@ll0w}

Mọi người cũng có thể tìm hiểu thêm về /robots.txt là thế nào thông qua bài post của Cookie Hân Hoan nhé ><

[https://www.facebook.com/cookie.han.hoan/posts/283664273758867](https://www.facebook.com/cookie.han.hoan/posts/283664273758867)

#### **4. Header 401**

![](<../.gitbook/assets/ảnh (23) (1).png>)

Thử vào đường dẫn thì trang web không có gì đặc biệt, trừ dòng "Hello GET request"

![](<../.gitbook/assets/ảnh (20).png>)

View source thử xem và chú ý 2 điểm sau

![](<../.gitbook/assets/ảnh (24) (1).png>)

Đầu tiên là mình đang sử dụng GET method, cái thứ 2 nó cho mình `Authorization `

Bạn có thể tham khảo thêm về cú pháp header Authorization tại [đây ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization)

Bài này thì mình chỉ việc thay đổi request method từ GET -> POST và thêm header `Authorization` là xong

Khi send với method POST thì cần thêm header `Content-Type: application/x-www-form-urlencoded `nhưng nếu bạn nào sử dụng BurpSuite thì có thể chuột phải và Change request method thì nó cũng sẽ tự thêm cho mình, tiện hơn.&#x20;

`Z2Fjb25sb250b246Y29va2llaGFuaG9hbg== `cái này chính là gaconlonton:cookiehanhoan base64 encode. Có 1 lưu ý là nhiều bạn quên việc change method, cũng như ghi sau cấu trúc header của Authorization dẫn tới việc bị sai và không cho ra kết quả.&#x20;

![](<../.gitbook/assets/ảnh (23).png>)

Flag{m4g1c@l\_h34d3r\_xD}

#### **5. Infinite Loop**

![](<../.gitbook/assets/ảnh (10).png>)

Ở bài này chúng ta lại có 1 form đăng nhập, nhưng với nội dung mô tả của chall này thì mình nghĩ nó không liên quan gì tới việc login đúng tên hay không. Thử nhập username/password bất kì và ấn login&#x20;

![](<../.gitbook/assets/ảnh (1).png>)

Dùng BurpSuite bắt reponse và kiểm tra, có thể thấy ở tab HTTP History, các id được check nhảy từ 0-9, thử gửi 1 request qua Repeater và kiểm tra nhé.&#x20;

![](<../.gitbook/assets/ảnh (24).png>)

Như thế này, cứ ấn Follow redirection để nó follow theo luồng tiếp thôi. Tới khoảng id=6 sẽ có flag.

Flag{Y0u\_c4ptur3\_m3\_xD!!!}

#### 6. JS B\*\*p B\*\*p

![](<../.gitbook/assets/ảnh (6).png>)

![](<../.gitbook/assets/ảnh (8).png>)

Ở bài này nó cho mình 1 form login thế này, với đề bài là JS thì mình nghĩ ngay đến việc view-source để xem thử có kèm file js nào không thì thấy có 4 file .js, nó hiện thị 1 chuỗi các kí tự lạ, mà với kinh nghiệm cá nhân thì mình nhận thấy liền là JSFUCK. Mọi người có thể dùng tool [JSFUCK](https://enkhee-osiris.github.io/Decoder-JSFuck/) đây để decode nó ra nhé. Và dưới đây là code sau khi mình đã beauty code từ 4 file js kia.

```
//File 1 .js
function verifyUsername(username) {
    if (username != "cookiehanhoan") {
        return false
    }
    return true
}

//File 2 .js
function reverseString(str) {
    if (str === "") {
        return ""
    } else {
        return reverseString(str.substr(1)) + str.charAt(0)
    }
}

//File 3 .js
function verifyPassword(password) {
    if (reverseString(password) != "dr0Wss@p3rucreSr3pus") {
        return false
    }
    return true
}

//File 4 .js
function verifyRole(role) {
    if (role.charCodeAt(0) != 64) {
        return false;
    }
    if ((role.charCodeAt(1) + role.charCodeAt(2) != 209) && (role.charCodeAt(2) - role.charCodeAt(1) != 9)) {
        return false
    }
    if ((role.charCodeAt(3).toString() + role.charCodeAt(4).toString() != "10578") && (role.charCodeAt(3) - role.charCodeAt(4) != 27)) {
        return false
    }
    return true
}
```

Ở file 1 .js: mình sẽ có username là cookiehanhoan

Ở file 2 và 3 .js: mình sẽ có 1 hàm `reverseString `thông qua đó mình cần reverse chuỗi `dr0Wss@p3rucreSr3pus -> sup3rSercur3p@ssW0rd `và đây cũng chính là password của mình

Ở file 4 .js: đoạn này phân tích code 1 xíu thì mình sẽ biết role là `@dmiN `, giải thích sơ qua 1 chút thì trường hợp 2 chuỗi 10 + 578 thì sẽ không hợp lí (mình còn xét điều kiện phía sau), cho nên mình sẽ lấy 105 + 78. Vậy suy ra charCodeAt(3) là 105 và charCodeAt(4) là 78, khi trừ nhau thì ra 27, đúng với điều kiện nhé :v.&#x20;

Còn charCodeAt(0) sẽ có giá trị ascii là 64, charCodeAt(1) và (2) thì áp dụng 1 chút toán, bấm máy hệ phương trình thì sẽ có kết quả lần lượt là 100 và 109. Từ đây suy ra role thôi bằng cách dò bảng Ascii từ những dữ kiện đã có thôi.&#x20;

Login với 3 thông tin đã có được, ta sẽ có flag.&#x20;

Flag{JAV-ascript\_F\*ck}

#### 7. Impossible

![](../.gitbook/assets/ảnh.png)

![](<../.gitbook/assets/ảnh (4).png>)

Bài này họ bảo mình nhập password để lấy flag, nhưng không có password gì cả, thì lại view-source để xem thì có 1 đoạn script js như sau:

![](<../.gitbook/assets/ảnh (28).png>)

Đoạn script này được sử dụng để kiểm tra password. Password chúng ta nhập sau khi được xóa bỏ đoạn “**cookiehanhoan**“, sẽ được đem đi mã hóa base64 và so sánh với **Y29va2llaGFuaG9hbg==**, mà đoạn này giải mã ra cũng chính là “**cookiehanhoan**”. Nói cách khác, mật khẩu chúng ta nhập sau khi lược bỏ đoạn “**cookiehanhoan**” vẫn phải có giá trị là “**cookiehanhoan**” thì mới hợp lệ.&#x20;

Hàm btoa chính là hàm Base64 encode password sau khi replace.

Password mình sẽ nhập vào là `cookiecookiehanhoanhanhoan. `Giải thích 1 chút ở chỗ này, sau khi nhập chuỗi password này vào, tới đoạn replace thì nó sẽ replace chuỗi `cookiehanhoan `ở giữa, và sau khi bị replace thì lúc này chỉ còn `cookie `và `hanhoan`, ghép lại ta được cookiehanhoan.

Flag{Javascript\_is\_not\_safe???}

