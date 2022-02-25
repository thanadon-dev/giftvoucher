# giftvoucher
แจก API วอเลทอั่งเปาสำหรับคนที่มีปัญหาเรื่อง Wallet แบน IP นอกก็ใช้ตัวนี้ได้ครับ

# PHP

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

# Golang

```golang
package main

import (
  "fmt"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://api.zmine.me/giftvoucher/กรอกรหัสอั่งเปา/กรอกเบอร์/"
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

# Nodejs

```nodejs
var axios = require('axios');

var config = {
  method: 'get',
  url: 'https://api.zmine.me/giftvoucher/111/097/',
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

# Dart

```dart
var request = http.Request('GET', Uri.parse('https://api.zmine.me/giftvoucher/111/097/'));

http.StreamedResponse response = await request.send();

if (response.statusCode == 200) {
  print(await response.stream.bytesToString());
}
else {
  print(response.reasonPhrase);
}
```

