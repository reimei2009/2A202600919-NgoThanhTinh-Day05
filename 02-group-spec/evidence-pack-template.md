# Evidence Pack - Vietnam Airlines NEO Baggage Allowance Checker

Nop kem thin SPEC cuoi Day 05.

## 1. Nhom va track

**Ten nhom:** Nhom NEO - Baggage Clarity  
**Track:** Travel / Airline customer support  
**Product/app da chon:** Vietnam Airlines - NEO virtual assistant va app Vietnam Airlines  
**Build slice dang nghi:** AI kiem tra va giai thich hanh ly da bao gom trong ve, truoc khi user mua them prepaid baggage.

## 2. Self-use evidence

Nhom tu dung workflow theo prompt gia lap vi khong co booking that de test payment/check-in end-to-end.

| Observation | Screenshot/link | Path lien quan | Dieu hoc duoc |
|---|---|---|---|
| Vietnam Airlines dinh vi chatbot AI la kenh ho tro tra cuu lich bay, thong tin hanh ly, check-in, hoan/doi ve va tinh huong co ban. | https://spirit.vietnamairlines.com/bay-cao-khat-vong-5-sao/chuyen-doi-so-vna/xay-dung-tro-ly-so-da-nen-tang-vietnam-airlines-nang-chuan-dich-vu-khach-hang-trong-ky-nguyen-so.html | Happy | NEO phu hop de xu ly cau hoi pho bien, nhung promise rong nen can cat thanh task co context ro. |
| Khi hoi "Toi co can mua them 1 kien 23kg khong?", neu AI chi dua chinh sach chung thi user van khong biet ve cua minh da co allowance hay chua. | Prompt gia lap cua nhom; can bo sung screenshot that khi co booking demo | Low-confidence | Task can booking context. AI khong nen ket luan neu thieu fare class/chang bay/allowance. |
| App Store version history cho thay app co tinh nang check baggage status, request refund va purchase baggage trong check-in. | https://apps.apple.com/us/app/vietnam-airlines/id1472323081 | Happy / Failure | Hanh ly, refund va check-in la workflow that trong app, khong phai y tuong ngoai he thong. |
| Complaint BBB mo ta app check-in khong hien allowance included, lam user mua prepaid baggage du da co hanh ly trong fare. | https://www.bbb.org/us/ca/san-francisco/profile/airlines/vietnam-airlines-1116-192652/complaints | Failure / Correction | Failure co tac dong tien that. Prototype can ngan mua trung va co recovery path. |

## 3. User / review / social evidence

| Quote / review / observation | Nguon | User la ai? | Pain/failure mode |
|---|---|---|---|
| User report rang mobile app check-in khong hien included baggage allowance, nen ho mua them prepaid bag; sau do refund bi tu choi. | BBB complaint, 23/06/2025: https://www.bbb.org/us/ca/san-francisco/profile/airlines/vietnam-airlines-1116-192652/complaints | Hanh khach da mua ve Economy Classic, check-in truoc chuyen bay | App/AI khong lam ro allowance theo booking, dan den mua trung dich vu. |
| Review noi app "time-consuming and inefficient" va user khong co thong tin ro ve flight/support. | Trustpilot review, 23/04/2026: https://www.trustpilot.com/review/vietnamairlines.com | Khach bay quoc te/noi dia can thong tin chuyen bay va support | Thieu thong tin hanh dong duoc, user bi bo trong trang thai khong chac. |
| Review khac noi chuyen bay noi dia bi doi gio 2.5 tieng nhung user khong duoc thong bao va chi phat hien khi den san bay. | Trustpilot review, 01/05/2026: https://www.trustpilot.com/review/vietnamairlines.com | Hanh khach bay noi dia | Workflow hang khong co nhieu thay doi theo context; AI can noi ro du lieu/nguon va muc do chac chan. |
| Vietnam Airlines noi chatbot xu ly cac yeu cau pho bien nhu hanh ly, check-in, hoan/doi ve va giup giam tai tong dai vien. | Spirit Vietnam Airlines, 05/03/2026: https://spirit.vietnamairlines.com/bay-cao-khat-vong-5-sao/chuyen-doi-so-vna/xay-dung-tro-ly-so-da-nen-tang-vietnam-airlines-nang-chuan-dich-vu-khach-hang-trong-ky-nguyen-so.html | Hanh khach can tu phuc vu nhanh | Co co hoi dung AI cho cau hoi lap lai, nhung phai chuyen nguoi that khi co tien/rui ro. |

## 4. Competitor / analog evidence

| App / mo hinh tham khao | Ho xu ly task nay the nao? | Pattern hoc duoc | Co ap dung trong 1 ngay khong? |
|---|---|---|---|
| Airline self-service baggage calculator | Yeu cau hanh trinh, fare/booking va so kien hanh ly truoc khi tinh phi | Lay context truoc khi dua khuyen nghi | Co, co the mock bang form + rule + AI explanation. |
| Banking/card dispute assistant | Neu lien quan den tien va du lieu khong khop, tao ticket/review thay vi tu ket luan | Human review cho case rui ro | Co, prototype chi can nut "Chuyen agent / Tao yeu cau kiem tra". |
| E-commerce checkout warning | Canh bao khi user mua trung goi/dich vu da co | Friction dung luc truoc payment | Co, hien banner "Ve cua ban co 1 kien 23kg included". |

## 5. Evidence -> Insight

```text
Evidence noi bat nhat:
Complaint BBB cho thay app check-in khong hien baggage allowance da bao gom trong fare, lam user mua them prepaid baggage va gap kho khi refund.

Insight:
User khong chi can "hoi chinh sach hanh ly".
That ra ho can mot cau tra loi co context theo booking de ra quyet dinh co nen mua them hay khong, vi sai o buoc nay co tac dong tien that va kho recover.

Opportunity:
AI co the giup bang cach augment quyet dinh mua hanh ly: thu thap context, giai thich allowance hien co, canh bao mua trung, va chuyen agent neu du lieu khong chac.
```

## 6. Evidence doi SPEC nhu the nao?

- [x] Doi user chinh.
- [x] Doi pain statement.
- [x] Doi build slice.
- [x] Doi Auto/Aug decision.
- [x] Doi 4 paths.
- [x] Doi failure mode.
- [x] Doi owner/test plan.

Ghi ro thay doi quan trong:

```text
Truoc evidence, nhom dinh build chatbot ho tro hang khong chung chung.
Sau evidence, nhom doi thanh AI baggage allowance checker cho hanh khach da co ve.
Ly do:
Evidence cho thay pain khong nam o viec khong co thong tin chinh sach, ma nam o viec user khong biet chinh sach nao ap dung cho booking cua minh. Neu AI/app sai o day, user co the mua trung dich vu va kho lay lai tien.
```
