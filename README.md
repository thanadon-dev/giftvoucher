# 🎁 Gift Voucher API

> **TrueMoney Gift Voucher API** - ระบบเติมเงินผ่านอั่งเปา TrueMoney Wallet
> api อั่งเปา api อั่งเปาวอเลทฟรี api เติมเงินอั่งเปาวอเลท

> [!IMPORTANT]
>  **อัพเดท!** เปลี่ยนโดเมนจาก `zmine.me` → `gateway.autozy.app`  
> กรุณาอัพเดท URL ใหม่ในโค้ดของคุณ

---

## 📍 API Endpoint

```
GET https://gateway.autozy.app/api/giftvoucher/{voucher_code}/{phone_number}/
```

### ตัวอย่างการใช้งาน

```bash
curl -X GET "https://gateway.autozy.app/api/giftvoucher/abc123xyz/0812345678/"
```

> 💡 **หมายเหตุ**: `voucher_code` คือค่าหลัง `?v=` จาก URL ของอั่งเปา
> 
> `https://gift.truemoney.com/campaign/?v=abc123xyz` → ใช้ `abc123xyz`

---

## 📋 Status Codes

| Code | Status | Message | คำอธิบาย |
|:----:|:------:|:--------|:---------|
| `200` | ✅ success | `SUCCESS_FOR_TOPUP` | ทำรายการเสร็จสิ้น |
| `100` | ❌ error | `VOUCHER_OUT_OF_STOCK` | ซองถูกใช้งานแล้ว |
| `101` | ❌ error | `VOUCHER_NOT_FOUND` | ไม่พบซองของขวัญ |
| `102` | ❌ error | `CANNOT_GET_OWN_VOUCHER` | ไม่สามารถใช้อั่งเปาตัวเอง |
| `103` | ❌ error | `CANNOT_GET_MORE_ONE` | รับซองได้เพียงคนเดียว |
| `104` | ❌ error | `PLEASE_FILL_CORRECT` | ข้อมูลไม่ถูกต้อง |
| `105` | ❌ error | `VOUCHER_EXPIRED` | ซองหมดอายุ |

---

## 📦 Response Format

### ✅ Success Response

```json
{
  "code": "200",
  "status": "success",
  "data": {
    "name": "ชื่อผู้เติม",
    "tel": "08x-xxx-xxxx",
    "amount": 100
  },
  "message": "คุณได้เติมเงินมา : 100.00 บาท"
}
```

### ❌ Error Response

```json
{
  "code": "100",
  "status": "error",
  "data": null,
  "message": "ลิงค์ซองของขวัญถูกใช้งานแล้ว",
  "message_en": "VOUCHER_OUT_OF_STOCK"
}
```

---

## � Code Examples

<details>
<summary><b>🔧 cURL</b></summary>

```bash
curl -s "https://gateway.autozy.app/api/giftvoucher/YOUR_VOUCHER_CODE/YOUR_PHONE/"
```

</details>

<details>
<summary><b>🐘 PHP</b></summary>

```php
<?php
function redeemVoucher($voucherCode, $phone) {
    $url = "https://gateway.autozy.app/api/giftvoucher/{$voucherCode}/{$phone}/";
    
    $ch = curl_init($url);
    curl_setopt_array($ch, [
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_TIMEOUT => 30,
        CURLOPT_FOLLOWLOCATION => true,
    ]);
    
    $response = curl_exec($ch);
    curl_close($ch);
    
    return json_decode($response, true);
}

// Usage
$result = redeemVoucher("abc123xyz", "0812345678");
print_r($result);
```

</details>

<details>
<summary><b>🟢 Node.js</b></summary>

```javascript
async function redeemVoucher(voucherCode, phone) {
  const url = `https://gateway.autozy.app/api/giftvoucher/${voucherCode}/${phone}/`;
  const response = await fetch(url);
  return response.json();
}

// Usage
const result = await redeemVoucher("abc123xyz", "0812345678");
console.log(result);
```

</details>

<details>
<summary><b>🐍 Python</b></summary>

```python
import requests

def redeem_voucher(voucher_code: str, phone: str) -> dict:
    url = f"https://gateway.autozy.app/api/giftvoucher/{voucher_code}/{phone}/"
    response = requests.get(url)
    return response.json()

# Usage
result = redeem_voucher("abc123xyz", "0812345678")
print(result)
```

</details>

<details>
<summary><b>🐹 Go</b></summary>

```go
package main

import (
    "encoding/json"
    "fmt"
    "io"
    "net/http"
)

func redeemVoucher(voucherCode, phone string) (map[string]interface{}, error) {
    url := fmt.Sprintf("https://gateway.autozy.app/api/giftvoucher/%s/%s/", voucherCode, phone)
    
    resp, err := http.Get(url)
    if err != nil {
        return nil, err
    }
    defer resp.Body.Close()
    
    body, _ := io.ReadAll(resp.Body)
    
    var result map[string]interface{}
    json.Unmarshal(body, &result)
    
    return result, nil
}

func main() {
    result, _ := redeemVoucher("abc123xyz", "0812345678")
    fmt.Printf("%+v\n", result)
}
```

</details>

<details>
<summary><b>🎯 Dart / Flutter</b></summary>

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

Future<Map<String, dynamic>> redeemVoucher(String voucherCode, String phone) async {
  final url = Uri.parse('https://gateway.autozy.app/api/giftvoucher/$voucherCode/$phone/');
  final response = await http.get(url);
  
  if (response.statusCode == 200) {
    return jsonDecode(response.body);
  }
  throw Exception('Failed to redeem voucher');
}

// Usage
void main() async {
  final result = await redeemVoucher("abc123xyz", "0812345678");
  print(result);
}
```

</details>

<details>
<summary><b>☕ Java</b></summary>

```java
import java.net.http.*;
import java.net.URI;

public class GiftVoucher {
    public static String redeemVoucher(String voucherCode, String phone) throws Exception {
        String url = String.format(
            "https://gateway.autozy.app/api/giftvoucher/%s/%s/", 
            voucherCode, phone
        );
        
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
            .uri(URI.create(url))
            .GET()
            .build();
            
        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        return response.body();
    }
    
    public static void main(String[] args) throws Exception {
        String result = redeemVoucher("abc123xyz", "0812345678");
        System.out.println(result);
    }
}
```

</details>

<details>
<summary><b>💎 Ruby</b></summary>

```ruby
require 'net/http'
require 'json'

def redeem_voucher(voucher_code, phone)
  url = URI("https://gateway.autozy.app/api/giftvoucher/#{voucher_code}/#{phone}/")
  response = Net::HTTP.get(url)
  JSON.parse(response)
end

# Usage
result = redeem_voucher("abc123xyz", "0812345678")
puts result
```

</details>

<details>
<summary><b>🦀 Rust</b></summary>

```rust
use reqwest;
use serde_json::Value;

async fn redeem_voucher(voucher_code: &str, phone: &str) -> Result<Value, reqwest::Error> {
    let url = format!(
        "https://gateway.autozy.app/api/giftvoucher/{}/{}/",
        voucher_code, phone
    );
    
    let response = reqwest::get(&url).await?.json::<Value>().await?;
    Ok(response)
}

#[tokio::main]
async fn main() {
    let result = redeem_voucher("abc123xyz", "0812345678").await.unwrap();
    println!("{:?}", result);
}
```

</details>

<details>
<summary><b>🔷 C#</b></summary>

```csharp
using System.Net.Http;
using System.Text.Json;

class GiftVoucher
{
    static async Task<Dictionary<string, object>> RedeemVoucher(string voucherCode, string phone)
    {
        using var client = new HttpClient();
        var url = $"https://gateway.autozy.app/api/giftvoucher/{voucherCode}/{phone}/";
        
        var response = await client.GetStringAsync(url);
        return JsonSerializer.Deserialize<Dictionary<string, object>>(response);
    }
    
    static async Task Main()
    {
        var result = await RedeemVoucher("abc123xyz", "0812345678");
        Console.WriteLine(result);
    }
}
```

</details>

---

##  Features

-  รองรับ TrueMoney Gift Voucher ทุกประเภท
-  Bypass Cloudflare Protection
-  Response เร็ว < 2 วินาที
-  รองรับ High Traffic

---

<p align="center">
  <sub>Thanadon-dev</sub>
</p>
