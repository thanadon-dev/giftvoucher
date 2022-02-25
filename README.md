# giftvoucher
วอเลทอั่งเปาสำหรับคนที่มีปัญหาเรื่อง Wallet แบน IP นอกก็ใช้ตัวนี้ได้ครับ

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
