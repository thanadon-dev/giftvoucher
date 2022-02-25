# giftvoucher
แจก API วอเลทอั่งเปาสำหรับคนที่มีปัญหาเรื่อง Wallet แบน IP นอกก็ใช้ตัวนี้ได้ครับ
https://api.zmine.me/giftvoucher/ลิ้งอั่งเปา/เบอร์ผู้รับเงิน/


# Errors & Success

| code     | status  | message_en              | message                             |
| -------- | ------- | ----------------------- | ----------------------------------- |
| 100      | error   | VOUCHER_OUT_OF_STOCK    | ลิงค์ซองของขวัญถูกใช้งานแล้ว             |
| 101      | error   | VOUCHER_NOT_FOUND       | ลิงค์ซองของขวัญไม่ถูกต้อง                |
| 102      | error   | CANNOT_GET_OWN_VOUCHER  | ไม่สามารถใช้อั่งเปาของตัวเองได้            |
| 103      | error   | CANNOT_GET_MORE_ONE     | กรุณาเลือกให้รับซองได้เพียวคนเดียว         |
| 104      | error   | PLEASE_FILL_CORRECT     | เกิดข้อผิดพลาดกรุณากรอกข้อมูลให้ถูกต้อง     |
| 200      | success | SUCCESS_FOR_TOPUP       | ทำรายการเสร็จสิ้น                       |

# Response

```javascript
{
    "status": "success",                          //status ตอบกลับ
    "data": {                                     //โชว์ Data ถ้าหาก status เป็น error Data จะเป็น Null
        "name": "xxxx",                           //ชื่อผู้เติม
        "tel": "08x-xxx-xxx",                      //เบอร์ที่รับเงิน
        "amount": xx                              //จำนวนที่ได้รับ
    },
    "message": "คุณได้เติมเงินมา : xx.00 บาท",       //ข้อความตอบกลับ ภาษาไทย
    "message_en": "You have top-up : xx.00 baht" //ข้อความตอบกลับ อังกฤษ
}
```

# โค้ดสำหรับดึงรายการภาษา PHP

```php
$url = "ลิ้งอั่งเปา";
$tel = "กรอกเบอร์ผู้รับ";
function giftvoucher($url, $tel){
        $curl = curl_init();

        curl_setopt_array($curl, array(
        CURLOPT_URL => 'https://api.zmine.me/giftvoucher/'.$url.'/'.$tel.'/',
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_ENCODING => '',
        CURLOPT_MAXREDIRS => 10,
        CURLOPT_TIMEOUT => 0,
        CURLOPT_FOLLOWLOCATION => true,
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => 'GET',
        ));

        $response = curl_exec($curl);

        curl_close($curl);
        return $response;
    }
```

# โค้ดสำหรับดึงรายการภาษา Golang

```golang
package main

import (
  "fmt"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://api.zmine.me/giftvoucher/ลิ้งอั่งเปา/เบอร์ผู้รับเงิน/"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```

# โค้ดสำหรับดึงรายการภาษา Nodejs

```javascript
var axios = require('axios');

var config = {
  method: 'get',
  url: 'https://api.zmine.me/giftvoucher/ลิ้งอั่งเปา/เบอร์ผู้รับเงิน/',
  headers: { }
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});

```

# โค้ดสำหรับดึงรายการภาษา Dart

```dart
var request = http.Request('GET', Uri.parse('https://api.zmine.me/giftvoucher/ลิ้งอั่งเปา/เบอร์ผู้รับเงิน/'));

http.StreamedResponse response = await request.send();

if (response.statusCode == 200) {
  print(await response.stream.bytesToString());
}
else {
  print(response.reasonPhrase);
}
```

