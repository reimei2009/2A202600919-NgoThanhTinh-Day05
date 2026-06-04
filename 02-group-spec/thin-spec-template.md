# Thin SPEC Cuoi Day 05 - AI Baggage Allowance Checker

Thin SPEC khong phai PRD day du. Day la ban cam ket du ro de sang Day 06 nhom build ngay.

## 1. Track, product/app va user

**Track:** Travel / Airline customer support  
**Product/app that:** Vietnam Airlines - NEO virtual assistant va app Vietnam Airlines  
**User cu the:** Hanh khach pho thong da mua ve Vietnam Airlines, sap check-in, khong chac ve cua minh da bao gom hanh ly ky gui hay chua.  
**Nhom co phai user that khong? Neu khong, khac o dau?**  
Nhom co the la user gan dung vi deu co kha nang mua ve may bay va dung app/chatbot. Khac biet: nhom khong co booking Vietnam Airlines that tai thoi diem lam bai, nen Day 06 se dung booking data gia lap de demo.

## 2. Evidence summary

| Evidence | Nguon | User/pain noi len dieu gi? | SPEC phai doi gi? |
|---|---|---|---|
| Vietnam Airlines noi chatbot AI xu ly cac yeu cau pho bien nhu lich bay, hanh ly, check-in, hoan/doi ve va tinh huong co ban. | Spirit Vietnam Airlines, 05/03/2026: https://spirit.vietnamairlines.com/bay-cao-khat-vong-5-sao/chuyen-doi-so-vna/xay-dung-tro-ly-so-da-nen-tang-vietnam-airlines-nang-chuan-dich-vu-khach-hang-trong-ky-nguyen-so.html | Chatbot co vai tro that trong customer support, nhung scope rong can cat nho. | Chon mot workflow hep: baggage allowance truoc khi mua them. |
| App Store version history cho thay app co check baggage status, request refund, change flight khi schedule change, purchase baggage trong check-in. | App Store Vietnam Airlines: https://apps.apple.com/us/app/vietnam-airlines/id1472323081 | Hanh ly/refund/check-in la workflow that trong app. | Prototype nen gan voi man hinh check-in/mua them hanh ly. |
| Complaint BBB noi app check-in khong hien allowance included, user mua them prepaid baggage va bi tu choi refund. | BBB complaint, 23/06/2025: https://www.bbb.org/us/ca/san-francisco/profile/airlines/vietnam-airlines-1116-192652/complaints | Pain co tac dong tien that: mua trung dich vu va kho recover. | Failure mode chinh: AI/app lam user mua trung prepaid baggage. |
| Trustpilot review noi app mat thoi gian, khong hieu qua, thieu thong tin ro ve flight/support. | Trustpilot, 23/04/2026: https://www.trustpilot.com/review/vietnamairlines.com | User can thong tin hanh dong duoc va kenh recover khi khong chac. | Output phai co recommendation ro + human handoff. |

## 3. Pain statement

```text
User la hanh khach da mua ve Vietnam Airlines dang gap kho o buoc check-in/mua them hanh ly,
vi app/chatbot co the khong lam ro allowance nao da bao gom trong ve cua rieng user,
dan toi user mua them prepaid baggage du khong can, mat tien va kho refund.
Bang chung chinh la complaint BBB ngay 23/06/2025 ve viec mobile app check-in khong hien baggage allowance included, lam user mua them baggage du da co trong fare class.
```

## 4. Build slice

```text
Cho hanh khach pho thong da mua ve Vietnam Airlines dang check-in va khong chac co can mua them hanh ly,
prototype se dung AI de hoi 3 thong tin toi thieu va giai thich allowance theo booking gia lap,
tao ra khuyen nghi "khong can mua / nen mua them / can agent kiem tra",
va xu ly failure mode "user sap mua trung prepaid baggage" bang canh bao truoc payment, dan nguon chinh sach va nut chuyen agent.
```

## 5. Auto/Aug decision

Chon mot:

- [x] **Augmentation:** AI goi y/draft/phan loai, user quyet cuoi.
- [ ] **Conditional automation:** AI tu lam trong case hep; case mo ho/rui ro chuyen nguoi.
- [ ] **Automation:** AI tu quyet va tu hanh dong.

**Ly do chon:**  
Task lien quan den tien, chinh sach ve va refund. AI khong nen tu mua them hanh ly hay tu ket luan neu du lieu booking khong du. AI chi nen giai thich, canh bao, va de user/agent quyet dinh.

**Human role:** decider + rescuer. User quyet dinh co mua hay khong; agent xu ly khi du lieu khong khop, user da mua nham, hoac case can refund.

## 6. Four paths

| Path | Prototype phai the hien gi? |
|---|---|
| Happy | User nhap booking gia lap co Economy Classic, 1 kien 23kg included, muon mang 1 kien 20kg. AI tra loi "khong can mua them", hien allowance, ly do va link/chinh sach. |
| Low-confidence | User khong co ma dat cho/fare class hoac thong tin booking thieu. AI hoi lai 3 truong bat buoc, khong dua khuyen nghi mua them. |
| Failure | Booking data gia lap bi conflict: fare noi co 1 kien included nhung app purchase flow goi y mua them. AI hien canh bao "co kha nang mua trung" va yeu cau agent review. |
| Correction | User bam "Ket qua nay sai / Toi da mua nham". Prototype luu correction trong log demo va hien buoc tiep theo: tao yeu cau kiem tra/refund, kem thong tin can chuan bi. |

## 7. Failure mode nguy hiem nhat

```text
Neu user dang check-in va hoi "toi co can mua them 1 kien 23kg khong?",
AI co the bo qua allowance included trong fare class va khuyen nghi mua them prepaid baggage,
hau qua la user bi tinh phi cho dich vu da co san, sau do kho refund va mat niem tin vao app/chatbot.
Prototype se xu ly bang:
- bat buoc lay booking context truoc khi khuyen nghi,
- hien bang so sanh "allowance da co" vs "hanh ly user muon mang",
- canh bao neu user sap mua trung,
- show source/chinh sach,
- chuyen agent khi confidence thap hoac du lieu conflict.
Owner kiem thu path nay la Ngo Thanh Tinh.
```

## 8. Owner plan cho sang Day 06

| Thanh vien | Viec phu trach | Bang chung can co trong repo |
|---|---|---|
| Ngo Thanh Tinh | Research / evidence | Evidence pack co link BBB, Trustpilot, App Store, Spirit Vietnam Airlines. |
| Ngo Thanh Tinh | SPEC | Thin SPEC da dien day du pain, build slice, 4 paths, failure mode. |
| Ngo Thanh Tinh | Prototype | Demo web/app mock: form booking + AI explanation panel + recommendation. |
| Ngo Thanh Tinh | Test / failure path | Test cases cho happy, low-confidence, failure, correction. |
| Ngo Thanh Tinh | Demo script / repo | README Day 06, anh man hinh demo, video/gif neu kip. |

## 9. Prototype scope cho Day 06

### In scope

- Form nhap thong tin gia lap: booking code, fare class, route, so kien/soc kg user muon mang.
- Dataset mock 3 booking:
  - Happy: Economy Classic co 1 kien 23kg included.
  - Need buy: Economy Lite khong co checked baggage, user can 1 kien 20kg.
  - Conflict: app goi y mua baggage nhung fare data noi da included.
- AI/rule hybrid explanation:
  - Rule tinh allowance va warning.
  - AI viet explanation ngan, de hieu, co tone support.
- 4 path demo day du.

### Out of scope

- Ket noi API booking that.
- Thanh toan baggage that.
- Refund thật.
- Multi-airline/codeshare.
- Luu correction vao he thong that.

## 10. Prompt/logic goi y neu dung AI API

Neu Day 06 can dung LLM, chi can mot provider OpenAI-compatible. Khong commit `.env`.

```text
System:
Ban la tro ly ho tro hanh ly cua Vietnam Airlines trong prototype giao duc.
Chi dua khuyen nghi dua tren booking_data duoc cung cap.
Neu thieu thong tin hoac du lieu conflict, khong duoc ket luan; hay hoi lai hoac chuyen agent.
Khong tu tao chinh sach. Luon noi ro day la prototype va can user/agent xac nhan voi case lien quan den tien/refund.

User:
booking_data={{booking_data}}
user_baggage={{user_baggage}}
Hay tra loi bang 4 phan:
1. Ket luan ngan
2. Vi sao
3. User nen lam gi tiep
4. Khi nao can gap agent
```
