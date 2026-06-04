# Synthesis - Tu Evidence Den Build Slice

Dung sau khi nhom da co evidence. Muc tieu la chot mot build slice du nho cho Day 06.

## 1. Gom evidence thanh cum

Gom theo workflow/pain, khong gom theo ten feature.

| Cum evidence | Evidence | Product implication |
|---|---|---|
| Khong biet allowance nao ap dung cho booking cua minh | BBB complaint: app check-in khong hien baggage allowance included, user mua them prepaid bag | Prototype phai lay booking/fare context truoc khi khuyen nghi mua them. |
| Thieu thong tin hanh dong duoc trong app/support | Trustpilot review noi app mat thoi gian, khong hieu qua, kho lien he support | Output phai ngan, ro buoc tiep theo, co nut chuyen agent. |
| Chatbot duoc ky vong xu ly FAQ quy mo lon | Spirit Vietnam Airlines noi chatbot xu ly hanh ly, check-in, hoan/doi ve | AI phu hop cho task lap lai, nhung chi nen augment quyet dinh cua user. |
| Workflow co lien quan den tien va refund | App Store version history co refund/request baggage; complaint ve prepaid baggage | Can failure path va correction path, khong chi happy path. |

## 2. Viet insight

```text
Hanh khach da mua ve khong chi can doc chinh sach hanh ly.
Ho that ra can biet "ve cua toi da bao gom gi va toi co dang sap mua trung khong",
vi evidence cho thay app/support co the khong lam ro allowance theo booking, dan den quyet dinh mua them sai va kho recover.
```

## 3. Viet opportunity

```text
Co hoi la dung AI de augment quyet dinh mua hanh ly them,
giup hanh khach hieu allowance hien co va buoc tiep theo,
trong khi van kiem soat rui ro bang cach khong tu ket luan khi thieu booking context, dan nguon, va chuyen agent voi case tien/refund.
```

## 4. Chon build slice

Build slice:

```text
Cho hanh khach pho thong da mua ve Vietnam Airlines va dang check-in/mua them hanh ly,
prototype dung AI de hoi 3 thong tin toi thieu, giai thich allowance theo booking gia lap,
tao ra khuyen nghi "khong can mua / nen mua them / can agent kiem tra",
va xu ly failure "app/AI lam user mua trung prepaid baggage" bang canh bao mua trung + nut chuyen agent/review.
```

Kiem tra 5 cau hoi:

| Cau hoi | Dat chua? | Ghi chu |
|---|---|---|
| User cu the chua? | Dat | Hanh khach da mua ve, dang check-in hoac can mua them hanh ly. |
| Task du hep chua? | Dat | Chi xu ly mot cau hoi: co can mua them hanh ly khong. |
| AI decision ro chua? | Dat | AI giai thich allowance va dua khuyen nghi co/khong/can agent. |
| Failure path ro chua? | Dat | AI/app khong nhan ra allowance included -> user mua trung prepaid baggage. |
| Co evidence khong? | Dat | BBB, Trustpilot, App Store, Spirit Vietnam Airlines. |

## 5. Quyet dinh: giu, giam scope, hay doi huong?

| Tinh huong | Quyet dinh cua nhom |
|---|---|
| Evidence yeu, user mo ho | Khong xay ra. Evidence du de chot pain ve baggage allowance. |
| Y tuong qua rong | Da giam scope tu "AI airline assistant" xuong "baggage allowance checker". |
| AI khong can thiet | AI co ich de dien giai policy theo ngon ngu user, nhung du lieu booking trong prototype se mock/rule-based. |
| Rui ro cao | Chon augmentation: AI goi y, user quyet cuoi, case mo ho chuyen agent. |
| Khong demo duoc trong 1 ngay | Backlog cac tinh nang tich hop booking thật/payment thật/refund thật. |

## 6. Cau chot cuoi

```text
Dua tren evidence tu BBB, Trustpilot, App Store va thong tin Vietnam Airlines ve NEO,
nhom se build prototype slice "AI baggage allowance checker",
cho hanh khach da mua ve Vietnam Airlines,
de giai quyet pain khong biet ve cua minh da co hanh ly hay can mua them,
bang cach AI hoi context, giai thich allowance va canh bao mua trung,
va se test failure path "AI/app lam user mua trung prepaid baggage".
```

## 7. Backlog

Nhung thu khong build trong Day 06:

- Tich hop API booking/PNR that cua Vietnam Airlines.
- Thanh toan mua hanh ly that.
- Tao refund request that.
- Luu correction vao CRM/knowledge base that.
- Ho tro tat ca hang ve, chang bay quoc te, partner airlines va codeshare.
- Da ngon ngu day du Viet/Anh/Han/Nhat.
