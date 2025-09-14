# VahanaTTS (VITS Models)

## การใช้งาน (ภาษาไทย)

VahanaTTS เป็นระบบ Text-to-Speech (TTS) ที่ใช้โมเดล VITS ซึ่งช่วยให้คุณสามารถแปลงข้อความเป็นเสียงได้อย่างรวดเร็ว รองรับการใช้งานทั้งบน GPU และ CPU
- โมเดล fintune จาก [MMS-TTS-THA](https://huggingface.co/facebook/mms-tts-tha)
   
---

## 1. การติดตั้ง

### ขั้นตอนการติดตั้ง
1. เปิด Command Prompt หรือ Terminal
2. ใช้คำสั่งต่อไปนี้:

```sh
git clone https://github.com/VYNCX/VachanaTTS.git
cd VachanaTTS
pip install -r requirements.txt
///GPU Usage
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

3. รันไฟล์ `install.bat` เพื่อติดตั้งโปรแกรม:
   - หากต้องการใช้งาน GPU ให้พิมพ์ `y` (ต้องใช้ NVIDIA CUDA)
     - **ข้อดี**: รวดเร็ว
     - **ข้อเสีย**: ใช้ทรัพยากรเครื่องและพื้นที่เยอะ
   - หากต้องการใช้งาน CPU ให้พิมพ์ `n`
     - **ข้อดี**: ประหยัดพื้นที่และทรัพยากร
     - **ข้อเสีย**: ช้ากว่า โดยเฉพาะหากใช้งานโหมดโคลนเสียง

---

## 2. การใช้งาน

### เริ่มต้นใช้งาน
1. รันคำสั่งต่อไปนี้ใน Command Prompt หรือ Terminal:

```sh
python app.py
```
ภาษาไทย
```sh
python app-th.py
```
หรือ

2. เปิดไฟล์ `app.bat` เพื่อเริ่มโปรแกรม ,ภาษาไทยเปิด `app-th.bat`

---

3. ใช้งานบน [Google Colab](https://colab.research.google.com/drive/1LgHAUJFxNx7ReyQo9FUVJfYmqQ6XPQdk?usp=sharing)

## 3. ดาวน์โหลดโมเดล

ก่อนใช้งาน จำเป็นต้องดาวน์โหลดโมเดลจาก [Huggingface](https://huggingface.co) ตัวอย่างโมเดล:

[VIZINTZOR - Huggingface](https://huggingface.co/VIZINTZOR)

1. ดาวน์โหลดโมเดลที่ต้องการ
2. วางไฟล์โมเดลในโฟลเดอร์ `models` ของโปรเจกต์

- หากใช้การโคลนเสียง ดาวน์โหลดโมเดล [OpenVoice](https://github.com/VYNCX/OpenVoice-WebUI/releases/download/Download/OPENVOICE_MODELS.zip) แตกไฟล์ และ วางไฟล์โมเดลในโฟลเดอร์ `OPENVOICE_MODELS` ของโปรเจกต์
---

## 4. Finetune โมเดล ด้วย dataset ของตัวเอง

[Finetune ใน Google Colab](https://colab.research.google.com/drive/12qbpHnu7wYiTEoqh6_57_KUjp4gJkx2h?usp=sharing)

หรือ 

รันไฟล์ `finetune-webui.bat` เพื่อ Finetune โมเดล ด้วย Webui

ตัวอย่างการเตรียม Dataset 
   - รองรับเสียงความยาว 3-15 วินาที ต่อ 1 เสียง
   - แนะนำ ไฟล์เสียง อย่างน้อย 10-20 เสียง ในการ Finetune

**ตัวอย่าง Dataset** 
```text
/dataset
 /TH_MALE
 - metadata.csv
 - /audio
   - /audio1.wav
```
ไฟล์ Metadata.csv

```text
file_name,text
audio/audio1.wav,สวัสดีครับทุกคน ยินดีที่ได้พบกันอีกครั้ง
audio/audio2.wav,เธอเคยเห็นนกบินสูงบนฟ้าสีครามไหม
```

## ตัวอย่างการใช้งาน WEBUI

- พอดแคสต์ ตัวอย่างข้อความ Speaker 1 แทนผู้พูด 1 จากโมเดลเสียง ตัวอย่าง
```text
Speaker 1 : สำหรับพอดแคสต์ในวันนี้ เราจะมาพูดคุยกันเกี่ยวกับหัวข้อที่หลายคนอาจจะสนใจครับ
Speaker 2 : ใช่ค่ะ หัวข้อในวันนี้คือ "การสร้างแรงบันดาลใจในชีวิตประจำวัน" ซึ่งหวังว่าทุกคนจะได้ไอเดียดี ๆ กลับไปนะคะ
```

- วิดีโอ Dubbing ใช้ 1, เพื่อลำดับผู้พูด และตามด้วยคำพูด จาก ไฟล์ srt
   - ถ้าไม่ใช้ ลำดับผู้พูดก็ไม่จำเป็นต่องใส่ด้านหน้าความ แต่จะใช้ได้เพียง โมเดลเสียงเดียวเท่านั้น
   - สามารถนำเสียงที่ต้องการโคลนมาใส่เพื่อโคลนเสียงให้เข้ากับเสียงในวิดีโอนั้น(อาจใช้เวลานานในการประมวลผล หากใช้การโคลนเสียง) หรือ ไม่ใช้การโคลนเสียงก็ได้

- ตัวอย่าง SRT ไฟล์
```srt
1
00:00:00,009 --> 00:00:03,336
1, ใครจากนักแสดงที่ทำให้คุณหัวเราะมากที่สุด?

2
00:00:03,643 --> 00:00:04,224
2, คุณ.

3
00:00:07,841 --> 00:00:10,555
2, งานแรกของคุณคืออะไร?
```

## อ้างอิง

- https://github.com/ylacombe/finetune-hf-vits
- https://github.com/myshell-ai/OpenVoice






