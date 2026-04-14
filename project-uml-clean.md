# UML Bản Dễ Đọc (Giảm Rối)

Tài liệu này là phiên bản UML tinh gọn để đọc nhanh.  
Bản đầy đủ vẫn nằm ở: `docs/project-uml-complete.md`.

---

## Cách đọc đề xuất

1. Xem **Sơ đồ 1** để nắm kiến trúc tổng thể.
2. Xem **Sơ đồ 2** để hiểu luồng request server.
3. Xem **Sơ đồ 3** để hiểu model dùng chung.
4. Xem **Sơ đồ 4** để hiểu client UI.
5. Xem **Sơ đồ 5** để hiểu realtime.

> Nguyên tắc giảm rối: sơ đồ tổng quan **không nhét tất cả method**.  
> Method chi tiết xem ở file full.

---

## Sơ đồ 1 - Kiến trúc liên module

```mermaid
flowchart LR
  C[auction-client] <--> SH[auction-shared]
  S[auction-server] <--> SH
  C -->|Socket Request/Response| S
  S --> DB[(MySQL)]
```

---

## Sơ đồ 2 - Server request pipeline

```mermaid
flowchart LR
  SS[SocketServer] --> CH[ClientHandler]
  CH --> US[UserService]
  CH --> AM[AuctionManager]
  CH --> DAO1[ItemDao / LotDao / RatingDao / TransactionLogDao]
  AM --> BS[BidService]
  BS --> DAO2[BidDao + ItemDao]
  US --> UDAO[UserDao]
  DAO1 --> DBC[DatabaseConnection]
  DAO2 --> DBC
  UDAO --> DBC
  DBC --> DB[(MySQL)]
```

---

## Sơ đồ 3 - Shared domain model (chỉ quan hệ chính)

```mermaid
classDiagram
direction TB

class Entity
class User
class Admin
class Seller
class Bidder
class UserRole
class Item
class Art
class Electronics
class Vehicle
class ItemStatus
class BidTransaction
class Lot
class Rating
class Request
class Response
class TransactionLog
class ItemFactory

Entity <|-- User
Entity <|-- Item
Entity <|-- BidTransaction
User <|-- Admin
User <|-- Seller
User <|-- Bidder
Item <|-- Art
Item <|-- Electronics
Item <|-- Vehicle
User ..> UserRole
Item ..> ItemStatus
ItemFactory ..> Item
Request ..> User
Response ..> Item
Response ..> User
```

---

## Sơ đồ 4 - Client UI orchestration

```mermaid
flowchart TD
  MAIN[Main + SceneManager] --> AUTH[Welcome/Login/Register]
  AUTH --> KHUNG[KhungController]

  KHUNG --> TC[TrangChuController]
  KHUNG --> HI[HistoryController]
  KHUNG --> YI[YourItemController]
  KHUNG --> PR[ProfileController]
  KHUNG --> AD[AdminDashboardController]
  KHUNG --> II[ItemInformationController]

  TC --> IC[ItemCardController]
  II --> BF[BiddingFormController]
  II --> RF[RatingFormController]

  KHUNG --> SB[ThanhTimKiemController]
  SB --> UP[UserProfileController]
  PR --> TH[TransactionHistoryController]
  KHUNG --> AL[AddNewLotController]
```

---

## Sơ đồ 5 - Realtime events

```mermaid
sequenceDiagram
  participant S as AuctionManager/Service
  participant N as NetworkClient
  participant K as KhungController
  participant P as ProfileController
  participant NC as NotificationCenter

  S->>N: BALANCE_UPDATE(User)
  N->>P: updateBalanceDirectly(...)

  S->>N: NEW_BID_UPDATE(Item)
  N->>K: updateRealtimeUi(...)

  S->>N: OUTBID_NOTIFY(itemId)
  N->>NC: addNotification(...)
```

---

## Bảng chỉ mục class theo nhóm (để tìm nhanh)

| Nhóm | Class chính |
|---|---|
| Shared Core | `Entity`, `User`, `Item`, `BidTransaction`, `Request`, `Response` |
| Shared Subtypes | `Admin`, `Seller`, `Bidder`, `Art`, `Electronics`, `Vehicle` |
| Server Entry | `Main`, `SocketServer`, `ClientHandler` |
| Server Service | `AuctionManager`, `BidService`, `SettlementService`, `AuctionCloser`, `UserService` |
| Server DAO | `DatabaseConnection`, `UserDao`, `ItemDao`, `BidDao`, `LotDao`, `RatingDao`, `TransactionLogDao` |
| Client Core | `Main`, `SceneManager`, `ClientSession`, `NetworkClient` |
| Client Controllers | `KhungController`, `TrangChuController`, `ItemInformationController`, `ProfileController`, `AdminDashboardController`, `HistoryController`, `YourItemController`, `AddNewLotController`, `ThanhTimKiemController` |

---

## Khi nào dùng bản nào

- Dùng `project-uml-clean.md`: đọc nhanh, onboarding, review kiến trúc.
- Dùng `project-uml-complete.md`: tra cứu đầy đủ method/visibility.

