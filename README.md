# แนวทางการทำงาน ESP32-Simple-cookbook

## 1. ระบุตัวอย่างที่ใช้ ว่าเอามาจากตัวอย่างไหน
เลือกโปรเจค simple HTTPD server Example จาก show examples แล้วกด create

![สกรีนช็อต 2024-10-30 133053](https://github.com/user-attachments/assets/c919b54a-183f-4fed-8f3e-4172237d31d1)

## 2. ระบุว่า จะแก้ไขตรงไหนบ้าง เพื่ออะไร
  1.ไปที่ idf.py menuconfig ที่ example config ตั้งค่า WiFi SSID/password
  
  ![สกรีนช็อต 2024-10-30 133413](https://github.com/user-attachments/assets/6f5c077d-8913-4f8c-a026-739967afbdd7)

  2.เพิ่มโค้ด
  ```
//1 บรรทัด 25
#include "esp_adc/adc_cali.h"
#include "esp_adc/adc_cali_scheme.h"
#include "esp_adc/adc_oneshot.h"

//2 บรรทัด 51
char analogtxt[128];
int adc_raw;

//3 ตรง /* An HTTP GET handler */

    // อ่านค่าจาก ADC
    adc_oneshot_read(adc1_handle, ADC_CHANNEL_0, &adc_raw);
    // อัพเดท
    sprintf(analogtxt, "<H1> Voltage = %d </H1>", adc_raw);
    // ส่งข้อมูลไปยังผู้ใช้
    httpd_resp_send(req, analogtxt, HTTPD_RESP_USE_STRLEN);
    return ESP_OK;
 ```

## 3. แสดงขั้นตอนการทำ project
  เมื่อแก้ไขเสร็จให้กด built flash moniter เพื่อรับIP และนำไปค้นหาในแถบURL
  *ต้องใช้wifiเดีนยวกัน
   ![image](https://github.com/user-attachments/assets/096b6486-8a4d-4332-b87c-2f021a07b407)

## 4. แสดงผลการทำ project
   ![image](https://github.com/user-attachments/assets/2fee0cb9-7b11-4edd-bd30-d4208de50e84)

## 5. สรุปผลการทำ project
โปรเจคนี้เป็นการใช้งาน HTTP Server เพื่อทดสอบการทำงานของ GET และ POST ตามโค้ดที่เขียนบน esp32

