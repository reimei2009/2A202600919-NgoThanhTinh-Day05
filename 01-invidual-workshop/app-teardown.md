# Workshop - Mo App AI That

**San pham chon:** Vietnam Airlines - NEO virtual assistant / he sinh thai ho tro so  
**Nguoi thuc hien:** Ngo Thanh Tinh  
**Ngay lam:** 04/06/2026  
**Output:** finding note + sketch `as-is / to-be`

## 1. Chon mot san pham de dung thu

| San pham | AI feature | Cach truy cap |
|---|---|---|
| Vietnam Airlines - NEO | Tro ly ao ho tro hoi dap ve ve, hanh ly, check-in, hoan/doi ve, tinh huong co ban phat sinh | Website/app Vietnam Airlines va cac kenh so nhu Facebook/Zalo |

Ly do chon: day la mot AI feature gan voi workflow co rui ro that. Neu AI/chatbot tra loi chung chung ve hanh ly, hoan phi, doi ve, user co the mat tien, tre chuyen bay hoac khong biet khi nao can gap nguoi that.

## 2. Promise vs reality

### Product hua gi?

Theo bai viet noi bo Vietnam Airlines ngay 05/03/2026, chatbot AI duoc dinh vi nhu "tro ly so" xu ly cac yeu cau pho bien: tra cuu lich bay, thong tin hanh ly, check-in, chinh sach hoan doi ve va cac tinh huong co ban phat sinh. He thong duoc trien khai tren website, app, Facebook va Zalo de dam bao thong tin xuyen suot.

Nguon:

- https://spirit.vietnamairlines.com/bay-cao-khat-vong-5-sao/chuyen-doi-so-vna/xay-dung-tro-ly-so-da-nen-tang-vietnam-airlines-nang-chuan-dich-vu-khach-hang-trong-ky-nguyen-so.html
- https://testcdn.vietnamairlines.com/at/en/support/chatbot

### User nao duoc hua se duoc giup?

User chinh trong bai phan tich nay:

```text
Hanh khach pho thong da mua ve, sap bay, can biet minh co bao nhieu hanh ly ky gui/hanh ly xach tay va co can mua them hanh ly hay khong.
```

### Ky vong AI lam duoc task nao?

Ky vong NEO/AI co the:

- Hoi user lay ma dat cho, hang ve, chang bay va thoi diem bay.
- Giai thich allowance hien co bang ngon ngu de hieu.
- Canh bao neu user sap mua trung dich vu da co trong hang ve.
- Dan nguon chinh sach hoac chuyen nguoi that khi case lien quan den tien/hoan phi.

### Khi dung that, diem gay o dau?

Do khong co booking ca nhan de test end-to-end, self-use duoc lam theo dang prompt gia lap workflow:

```text
Toi mua ve Economy Classic cua Vietnam Airlines, app khong hien hanh ly ky gui. Toi co can mua them 1 kien 23kg khong?
```

Observation: flow ho tro hien tai co the tra loi duoc FAQ/chinh sach tong quat, nhung rui ro nam o viec user can quyet dinh theo booking cu the. Neu AI chi tra loi theo policy chung hoac day user sang man hinh mua hanh ly ma khong kiem tra allowance, user co the mua thua dich vu.

Evidence ngoai nhom ung ho diem gay:

- BBB co complaint ngay 23/06/2025: user noi mobile app check-in khong hien allowance da gom trong fare class, lam ho mua them prepaid baggage du bi co san allowance.
- Trustpilot co review ngay 23/04/2026 noi app "time-consuming and inefficient" va user khong co thong tin ro ve chuyen bay.
- App Store version history cho thay app co cac tinh nang lien quan truc tiep: check baggage status, request refund, change flight khi schedule change, purchase baggage trong check-in.

Nguon:

- https://www.bbb.org/us/ca/san-francisco/profile/airlines/vietnam-airlines-1116-192652/complaints
- https://www.trustpilot.com/review/vietnamairlines.com
- https://apps.apple.com/us/app/vietnam-airlines/id1472323081

## 3. Ve 4 paths

| Path | Cau hoi | Danh gia hien tai / observation |
|---|---|---|
| Happy | Khi AI dung va tu tin, user thay gi? | User hoi chinh sach hanh ly pho bien, AI tra loi allowance chung va dan link/chinh sach lien quan. |
| Low-confidence | Khi AI khong chac, he thong co hoi lai/chuyen nguoi khong? | Case booking cu the can ma dat cho/hang ve/chang bay. Neu thieu du lieu, AI can hoi lai thay vi dua cau tra loi chung. |
| Failure | Khi AI sai, user biet bang cach nao va sua the nao? | Failure nguy hiem: AI/app lam user nghi khong co hanh ly included, user mua them baggage va sau do refund kho. |
| Correction | Khi user sua, correction co duoc luu/log/hoc lai khong? | Nen co nut "Toi da co allowance trong ve" / "Ket qua nay sai" de ghi log case, tao ticket hoan phi hoac chuyen agent. |

## 4. Viet finding thanh quyet dinh product

```text
Khi hanh khach da mua ve hoi "toi co can mua them hanh ly khong?",
AI/product co nguy co tra loi theo FAQ chung hoac dua user sang purchase flow ma chua doi chieu allowance theo booking,
hau qua la user co the mua trung prepaid baggage, mat tien va ton cong khieu nai/hoan phi.
Loi thuoc layer data-tool + UX recovery + safety.
Nen sua bang low-confidence path: bat buoc thu thap booking context, hien "allowance da co" vs "can mua them", dan nguon/chinh sach, va chuyen agent neu case lien quan den refund hoac du lieu khong khop.
```

Finding nay se doi SPEC theo huong: khong build "AI chatbot du lich/hang khong" chung chung, ma build mot slice nho "AI baggage allowance checker" cho hanh khach da co ve.

## 5. Sketch as-is / to-be

### As-is

```text
User sap bay
  -> Mo app/chatbot hoi ve hanh ly
  -> AI/app tra loi FAQ hoac hien option mua hanh ly
  -> User khong biet fare da bao gom hanh ly hay chua
  -> User mua them baggage de "cho chac"
  -> Sau chuyen bay moi phat hien mua trung
  -> Gui email/khieu nai, kho recover
```

Diem gay:

- Khong buoc user cung cap booking context truoc khi dua ra loi khuyen mua them.
- Thong tin allowance va purchase flow co the bi tach nhau.
- Khong co recovery ro neu user da mua nham.

### To-be

```text
User sap bay
  -> Hoi AI: "Toi co can mua them hanh ly khong?"
  -> AI hoi 3 thong tin: ma dat cho/ve, chang bay, so kien muon mang
  -> AI kiem tra/nhan dien allowance theo fare class
  -> AI hien:
       1. Allowance da co
       2. Phan vuot neu co
       3. Khuyen nghi: khong mua / mua them / can agent kiem tra
       4. Link chinh sach va nut chuyen ho tro
  -> Neu du lieu khong khop: AI khong ket luan, tao low-confidence path
  -> Neu user bao sai: log correction va tao ticket hoan phi/agent review
```

## 6. Tu kiem truoc khi nop

- [x] Co evidence cu the tu nguon public: Vietnam Airlines/Spirit, App Store, BBB, Trustpilot.
- [x] Co du 4 paths: Happy, Low-confidence, Failure, Correction.
- [x] Finding duoc viet thanh product decision.
- [x] Sketch co as-is va to-be.
- [x] Co cau noi ro finding nay se doi SPEC: cat scope thanh "AI baggage allowance checker".
