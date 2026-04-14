# UML Toàn Bộ Project 

Tài liệu này là bản UML đầy đủ, ưu tiên:
- Có **đủ field + method** trong class diagram.
- Chia nhỏ theo module/package để tránh rối và lỗi render.

## Quy ước ký hiệu
- `+`: `public`
- `-`: `private`
- `#`: `protected`
- `~`: package-private

---

## 1) Shared Module - `com.auction.shared` - User Types

```mermaid
classDiagram
direction LR

class Entity {
  <<abstract>>
  -serialVersionUID: long
  #id: int
  #version: int
  +getId(): int
  +setId(id: int): void
  +getVersion(): int
  +setVersion(v: int): void
}

class User {
  <<abstract>>
  #username: String
  #fullName: String
  #password: String
  #email: String
  #age: String
  #phoneNumber: String
  #balance: double
  #active: boolean
  #locked: boolean
  #avatarUrl: String
  #moneySpent: double
  #itemsBought: int
  #moneyReceived: double
  #itemsSold: int
  #avgRating: double
  #totalRatings: int
  +User()
  +User(u: String, p: String, e: String, a: String, ph: String)
  +getRole(): UserRole
  +getUsername(): String
  +setUsername(u: String): void
  +getFullName(): String
  +setFullName(ans: String): void
  +getPassword(): String
  +setPassword(p: String): void
  +getEmail(): String
  +setEmail(e: String): void
  +getAge(): String
  +setAge(a: String): void
  +getPhoneNumber(): String
  +setPhoneNumber(ph: String): void
  +getBalance(): double
  +setBalance(b: double): void
  +isActive(): boolean
  +setActive(a: boolean): void
  +isLocked(): boolean
  +setLocked(l: boolean): void
  +getAvatarUrl(): String
  +setAvatarUrl(ans: String): void
  +getMoneySpent(): double
  +setMoneySpent(m: double): void
  +getItemsBought(): int
  +setItemsBought(i: int): void
  +getMoneyReceived(): double
  +setMoneyReceived(m: double): void
  +getItemsSold(): int
  +setItemsSold(i: int): void
  +getAvgRating(): double
  +setAvgRating(r: double): void
  +getTotalRatings(): int
  +setTotalRatings(r: int): void
}

class Admin {
  -serialVersionUID: long
  +Admin()
  +Admin(u: String, p: String, e: String, a: String, ph: String)
  +getRole(): UserRole
}

class Seller {
  -serialVersionUID: long
  +Seller()
  +Seller(u: String, p: String, e: String, a: String, ph: String)
  +getRole(): UserRole
}

class Bidder {
  -serialVersionUID: long
  +Bidder()
  +Bidder(u: String, p: String, e: String, a: String, ph: String)
  +getRole(): UserRole
}

class UserRole {
  <<enumeration>>
  +BIDDER
  +SELLER
  +ADMIN
}

Entity <|-- User
User <|-- Admin
User <|-- Seller
User <|-- Bidder
User ..> UserRole
```

---

## 2) Shared Module - `com.auction.shared` - Auction and Protocol Types

```mermaid
classDiagram
direction LR

class Item {
  <<abstract>>
  -serialVersionUID: long
  #name: String
  #description: String
  #startingPrice: double
  #currentPrice: double
  #startTime: LocalDateTime
  #endTime: LocalDateTime
  #maxPrice: double
  #sellerId: int
  #winnerId: int
  #status: ItemStatus
  #imageUrl: String
  #sellerUsername: String
  #sellerAvatarUrl: String
  #category: String
  +Item()
  +Item(res: String, ans: String, res1: double, ans1: double, res2: int)
  +calculateTax(): double
  +getCategory(): String
  +setCategory(res: String): void
  +getName(): String
  +setName(res: String): void
  +getDescription(): String
  +setDescription(res: String): void
  +getStartingPrice(): double
  +setStartingPrice(res: double): void
  +getCurrentPrice(): double
  +setCurrentPrice(res: double): void
  +getStartTime(): LocalDateTime
  +setStartTime(res: LocalDateTime): void
  +getEndTime(): LocalDateTime
  +setEndTime(res: LocalDateTime): void
  +getMaxPrice(): double
  +setMaxPrice(res: double): void
  +getSellerId(): int
  +setSellerId(res: int): void
  +getWinnerId(): int
  +setWinnerId(res: int): void
  +getStatus(): ItemStatus
  +setStatus(res: ItemStatus): void
  +getImageUrl(): String
  +setImageUrl(res: String): void
  +getSellerUsername(): String
  +setSellerUsername(res: String): void
  +getSellerAvatarUrl(): String
  +setSellerAvatarUrl(res: String): void
}

class Art {
  +Art()
  +Art(res: String, ans: String, res1: double, ans1: double, res2: int)
  +getCategory(): String
  +calculateTax(): double
}

class Electronics {
  +Electronics()
  +Electronics(res: String, ans: String, res1: double, ans1: double, res2: int)
  +getCategory(): String
  +calculateTax(): double
}

class Vehicle {
  +Vehicle()
  +Vehicle(res: String, ans: String, res1: double, ans1: double, res2: int)
  +getCategory(): String
  +calculateTax(): double
}

class ItemStatus {
  <<enumeration>>
  +PENDING
  +OPEN
  +CLOSED
  +RUNNING
  +FINISHED
  +PAID
  +CANCELED
}

class ItemFactory {
  +createItem(res: String): Item
}

class BidTransaction {
  -serialVersionUID: long
  #itemId: int
  #userId: int
  #bidValue: double
  #timestamp: LocalDateTime
  #maxAutoBid: double
  #autoBid: boolean
  #autoBidIncrement: double
  +BidTransaction()
  +BidTransaction(res: int, ans: int, res1: double)
  +getItemId(): int
  +setItemId(res: int): void
  +getUserId(): int
  +setUserId(ans: int): void
  +getBidValue(): double
  +setBidValue(res: double): void
  +getTimestamp(): LocalDateTime
  +setTimestamp(ans: LocalDateTime): void
  +getMaxAutoBid(): double
  +setMaxAutoBid(res: double): void
  +isAutoBid(): boolean
  +setAutoBid(ans: boolean): void
  +getAutoBidIncrement(): double
  +setAutoBidIncrement(res: double): void
}

class Lot {
  -serialVersionUID: long
  -id: int
  -itemId: int
  -title: String
  -description: String
  -bidValue: double
  -startTime: LocalDateTime
  -endTime: LocalDateTime
  -imageUrl: String
  -sellerUsername: String
  -sellerAvatarUrl: String
  -winnerUsername: String
  +Lot()
  +getId(): int
  +setId(i: int): void
  +getItemId(): int
  +setItemId(i: int): void
  +getTitle(): String
  +setTitle(t: String): void
  +getDescription(): String
  +setDescription(d: String): void
  +getBidValue(): double
  +setBidValue(v: double): void
  +getStartTime(): LocalDateTime
  +setStartTime(t: LocalDateTime): void
  +getEndTime(): LocalDateTime
  +setEndTime(t: LocalDateTime): void
  +getImageUrl(): String
  +setImageUrl(u: String): void
  +getSellerUsername(): String
  +setSellerUsername(s: String): void
  +getSellerAvatarUrl(): String
  +setSellerAvatarUrl(s: String): void
  +getWinnerUsername(): String
  +setWinnerUsername(w: String): void
}

class Rating {
  -serialVersionUID: long
  -id: int
  -itemId: int
  -raterUserId: int
  -ratedUserId: int
  -stars: int
  -feedback: String
  -createdAt: LocalDateTime
  -raterUsername: String
  +Rating()
  +Rating(itemId: int, raterUserId: int, ratedUserId: int, stars: int, feedback: String)
  +getId(): int
  +setId(id: int): void
  +getItemId(): int
  +setItemId(res: int): void
  +getRaterUserId(): int
  +setRaterUserId(res: int): void
  +getRatedUserId(): int
  +setRatedUserId(res: int): void
  +getStars(): int
  +setStars(res: int): void
  +getFeedback(): String
  +setFeedback(res: String): void
  +getCreatedAt(): LocalDateTime
  +setCreatedAt(res: LocalDateTime): void
  +getRaterUsername(): String
  +setRaterUsername(res: String): void
}

class Request {
  -serialVersionUID: long
  +LOGIN: String
  +SIGNUP: String
  +BID: String
  +ADD: String
  +LIST: String
  +UPDATE_PROFILE: String
  +UPDATE_AVATAR: String
  +GET_ALL_USERS: String
  +LOCK_USER: String
  +UNLOCK_USER: String
  +ADD_LOT: String
  +GET_ONGOING_BIDS: String
  +GET_UPCOMING_BIDS: String
  +SUBMIT_RATING: String
  +GET_RATINGS: String
  +GET_PENDING_ITEMS: String
  +APPROVE_ITEM: String
  +REJECT_ITEM: String
  +GET_ITEM_BY_ID: String
  +PROMOTE_ADMIN: String
  +SEARCH_USERS: String
  +GET_USER_BY_ID: String
  +GET_ONGOING_LOTS: String
  #requestId: String
  #action: String
  #payload: Object
  #timestamp: LocalDateTime
  +Request(act: String, obj: Object)
  +getRequestId(): String
  +getAction(): String
  +getPayload(): Object
  +getTimestamp(): LocalDateTime
}

class Response {
  -serialVersionUID: long
  +OK: String
  +ERROR: String
  #requestId: String
  #status: String
  #message: String
  #payload: Object
  #timestamp: LocalDateTime
  +Response(rid: String, st: String, msg: String, obj: Object)
  +getRequestId(): String
  +getStatus(): String
  +getMessage(): String
  +getPayload(): Object
  +getTimestamp(): LocalDateTime
}

class TransactionLog {
  -serialVersionUID: long
  -id: int
  -userId: int
  -type: String
  -amount: double
  -itemId: int
  -createdAt: LocalDateTime
  +TransactionLog()
  +TransactionLog(u: int, t: String, a: double, i: int, c: LocalDateTime)
  +getId(): int
  +setId(res: int): void
  +getUserId(): int
  +setUserId(res: int): void
  +getType(): String
  +setType(res: String): void
  +getAmount(): double
  +setAmount(res: double): void
  +getItemId(): int
  +setItemId(res: int): void
  +getCreatedAt(): LocalDateTime
  +setCreatedAt(res: LocalDateTime): void
}

Entity <|-- Item
Entity <|-- BidTransaction
Item <|-- Art
Item <|-- Electronics
Item <|-- Vehicle
Item ..> ItemStatus
ItemFactory ..> Item
```

---

## 3) Server Module - `com.auction.server` + `com.auction.server.controller`

```mermaid
classDiagram
direction LR

class Main {
  +main(args: String[]): void
}

class SocketServer {
  -port: int
  -pool: ExecutorService
  +SocketServer(p: int)
  +startServer(): void
}

class ClientHandler {
  -socket: Socket
  -out: ObjectOutputStream
  -in: ObjectInputStream
  -userService: UserService
  -itemDao: ItemDao
  -lotDao: LotDao
  -logDao: TransactionLogDao
  -ratingDao: RatingDao
  -currentUser: User
  +ClientHandler(s: Socket)
  +getCurrentUser(): User
  +run(): void
  -process(req: Request): Response
  -handleSubmitRating(req: Request): Response
  -handleAddLot(req: Request): Response
  -handleDeposit(req: Request): Response
  +send(r: Response): void
}

ClientHandler ..|> Runnable
Main ..> SocketServer
SocketServer ..> ClientHandler
```

---

## 4) Server Module - `com.auction.server.service`

```mermaid
classDiagram
direction LR

class UserService {
  -userDao: UserDao
  +UserService()
  +login(u: String, p: String): User
  +signup(u: User): boolean
  +updateProfile(userId: int, fullName: String, email: String, phone: String): String
  +updateAvatar(username: String, ans: String): void
  +getAllUsers(): List~User~
  +setUserLocked(username: String, lockStatus: boolean): boolean
  +setUserRole(username: String, role: String): boolean
}

class BidService {
  -itemDao: ItemDao
  -bidDao: BidDao
  +BidService()
  +placeBid(b: BidTransaction): Response
}

class AuctionManager {
  -instance: AuctionManager
  -clients: List~ClientHandler~
  -bidservice: BidService
  -itemDao: ItemDao
  -userDao: UserDao
  -logDao: TransactionLogDao
  -autobids: Map~Integer, PriorityQueue~BidTransaction~~
  -AuctionManager()
  +getInstance(): AuctionManager
  +addClient(c: ClientHandler): void
  +removeClient(c: ClientHandler): void
  +processBid(b: BidTransaction): Response
  -registerAutoBidQueue(b: BidTransaction): void
  -tryProcessAutoCounters(itemId: int): void
  -getPreviousHighestBidder(id: int): int
  +sendToUser(id: int, r: Response): void
  +broadcast(r: Response): void
}

class AuctionCloser {
  -itemDao: ItemDao
  -bidDao: BidDao
  -scheduler: ScheduledExecutorService
  +AuctionCloser()
  +start(): void
}

class SettlementService {
  -itemDao: ItemDao
  -userDao: UserDao
  -logDao: TransactionLogDao
  +SettlementService()
  +start(): void
  -settle(res: Item): void
  -getWinnerId(id: int): int
}

AuctionManager ..> BidService
```

---

## 5) Server Module - `com.auction.server.dao`

```mermaid
classDiagram
direction LR

class DatabaseConnection {
  -instance: DatabaseConnection
  -connection: Connection
  -url: String
  -user: String
  -pass: String
  -DatabaseConnection()
  +getInstance(): DatabaseConnection
  +getConnection(): Connection
}

class UserDao {
  -conn: Connection
  +UserDao()
  -ensureProfileColumns(): void
  +login(u: String, p: String): User
  +signup(u: User): boolean
  -ensureUniqueIndexes(): void
  -indexExists(tableName: String, indexName: String): boolean
  -columnExists(tableName: String, columnName: String): boolean
  -existsDuplicateUser(username: String, email: String): boolean
  -normalize(value: String): String
  +updateUserProfile(userId: int, fullName: String, email: String, phone: String): String
  -emailTakenByOtherUser(userId: int, email: String): boolean
  -phoneTakenByOtherUser(userId: int, phone: String): boolean
  +updateAvatar(username: String, ans: String): void
  +setUserLocked(username: String, lockStatus: boolean): boolean
  +setUserRole(username: String, role: String): boolean
  +getAllUsers(): List~User~
  +updateBalance(id: int, b: double): boolean
  +addBidderMetrics(userId: int, amount: double): boolean
  +addSellerMetrics(userId: int, amount: double): boolean
  +searchUsers(keyword: String): List~User~
  +getById(id: String): User
}

class ItemDao {
  -conn: Connection
  +ItemDao()
  -ensureColumns(): void
  -columnExists(res: String, ans: String): boolean
  +getAll(): List~Item~
  +getById(res: int): Item
  +updatePrice(res: int, ans: double, res1: int): boolean
  +updateEndTime(res: int, ans: LocalDateTime): boolean
  +insertLot(res: String, ans: String, res1: double, ans1: double, res2: LocalDateTime, ans2: LocalDateTime, res3: String, ans3: String, res4: String): boolean
  +closeAuction(res: int, ans: int, res1: String): void
  -mapResultSet(res: ResultSet): Item
  +getExpiredItems(): List~Item~
  +getBySellerId(res: int): List~Item~
  +getPendingItems(): List~Item~
  +approveItem(res: int): boolean
  +rejectItem(res: int): boolean
  +getStatusStats(): HashMap~String, Integer~
  +getCategoryStats(): HashMap~String, Double~
}

class BidDao {
  -conn: Connection
  +BidDao()
  +placeBid(b: BidTransaction): boolean
  +addBid(b: BidTransaction): boolean
  +getByItem(iid: int): List~BidTransaction~
  +getWinner(iid: int): BidTransaction
}

class LotDao {
  -conn: Connection
  +LotDao()
  +getOngoingBids(userId: int): List~Lot~
  +getUpcomingBids(userId: int): List~Lot~
  +getClosedBids(userId: int): List~Lot~
  +getPastBids(userId: int): List~Lot~
  -mapResultSet(rs: ResultSet): Lot
}

class RatingDao {
  -conn: Connection
  +RatingDao()
  -ensureTable(): void
  +insertRating(r: Rating): boolean
  +hasRated(itemId: int, userId: int): boolean
  +getByItemId(itemId: int): List~Rating~
  +recalcUserRating(userId: int): void
}

class TransactionLogDao {
  -conn: Connection
  +TransactionLogDao()
  +insertLog(u: int, t: String, a: double, i: int): boolean
  +getByUserId(u: int): List~TransactionLog~
}

UserDao ..> DatabaseConnection
ItemDao ..> DatabaseConnection
BidDao ..> DatabaseConnection
LotDao ..> DatabaseConnection
RatingDao ..> DatabaseConnection
TransactionLogDao ..> DatabaseConnection
```

---

## 6) Client Module - `com.auction.client` Core

```mermaid
classDiagram
direction LR

class Main {
  +start(primaryStage: Stage): void
  +main(args: String[]): void
}

class App {
  +main(args: String[]): void
}

class SceneManager {
  -rootStage: Stage
  -GLOBAL_STYLE: String
  +setStage(stage: Stage): void
  +getStage(): Stage
  +switchScene(fxmlPath: String): void
}

class ClientSession {
  -currentUser: User
  -fullName: String
  -email: String
  -phone: String
  -activeRole: UserRole
  -ClientSession()
  +setCurrentUser(user: User): void
  +getCurrentUser(): User
  +getUsername(): String
  +getFullName(): String
  +getEmail(): String
  +getPhone(): String
  +getActiveRole(): UserRole
  +updateProfile(newFullName: String, newEmail: String, newPhone: String): String
  +updateAvatar(ans: String): void
  +toggleRole(): void
  +clear(): void
  -safe(value: String): String
}

Main <|-- Application
App ..> Main
Main ..> SceneManager
ClientSession ..> User
```

---

## 7) Client Module - `com.auction.client.app` + `com.auction.client.network`

```mermaid
classDiagram
direction LR

class NodeManager {
  +addNodeToPane(loader: NodeContentLoader, backGroundFrame: Pane): void
  +switchNodewithNode(node1: Node, node2: Node, backGroundFrame: Pane): void
  +removeNodeFromPane(node1: Node, backGroundFrame: Pane): void
}

class NodeContentLoader {
  -currentNode: T
  -controller: Object
  +load(fxmlPath: String): void
  +getCurrentNode(): T
  +getController(): C
}

class NetworkClient {
  -instance: NetworkClient
  -socket: Socket
  -out: ObjectOutputStream
  -in: ObjectInputStream
  -pendingMap: ConcurrentHashMap~String, LinkedBlockingQueue~Response~~
  -NetworkClient()
  +getInstance(): NetworkClient
  -startListener(): void
  -handleIncoming(res: Response): void
  +sendRequestAndWait(req: Request): Response
  +uploadFile(urlString: String, fileBytes: byte[]): String
}

NodeManager ..> NodeContentLoader
NetworkClient ..> Response
NetworkClient ..> Request
```

---

## 8) Client Module - `com.auction.client.controller`

```mermaid
classDiagram
direction LR

class AuthController {
  -out: ObjectOutputStream
  -in: ObjectInputStream
  -p: Pattern
  +isValidEmail(email: String): boolean
  +AuthController(out: ObjectOutputStream, in: ObjectInputStream)
  +login(u: String, pass: String): Response
  +register(u: String, pass: String, cp: String, e: String, age: String): Response
  -sendToServer(request: Request): Response
}

class LoginController {
  -rootPane: AnchorPane
  -u: TextField
  -p: PasswordField
  -ans: Label
  -initialize(): void
  +handleLogin(e: ActionEvent): void
  +back(e: ActionEvent): void
  +toRegister(e: ActionEvent): void
}

class RegisterController {
  -rootPane: AnchorPane
  -u: TextField
  -e: TextField
  -a: TextField
  -p: PasswordField
  -cp: PasswordField
  -ans: Label
  -initialize(): void
  +handleRegister(ev: ActionEvent): void
  +back(ev: ActionEvent): void
  +goWelcome(ev: ActionEvent): void
}

class WelcomeController {
  +toLogin(e: ActionEvent): void
  +toRegister(e: ActionEvent): void
}
```

---

## 9) Client Module - `com.auction.client.ui.Main`

```mermaid
classDiagram
direction LR

class KhungController {
  -instance: KhungController
  -mainContentPane: Pane
  -currentContentNode: Node
  -searchKeyword: String
  -categoryFilter: String
  -filterMinPrice: double
  -filterMaxPrice: double
  +itemDetailController: ItemInformationController
  -an: Node
  -hn: Node
  -mn: Node
  -pn: Node
  -adn: Node
  -aln: Node
  -tc: TrangChuController
  -yc: YourItemController
  -hc: HistoryController
  -SearchContainer: HBox
  -ContentArea: StackPane
  -AuctionMenu: HBox
  -HistoryMenu: HBox
  -MyItemMenu: HBox
  -ProfileMenu: HBox
  -ManageUsersMenu: HBox
  -UserName: Label
  -Rank: Label
  -primaryactionbutton: Button
  -sidebaravatar: ImageView
  +initialize(): void
  +openAuction(e: MouseEvent): void
  +openHistory(e: MouseEvent): void
  +openMyItems(e: MouseEvent): void
  +openProfile(e: MouseEvent): void
  +openManageUsers(e: MouseEvent): void
  +handleRefresh(e: ActionEvent): void
  +handlePrimaryAction(e: ActionEvent): void
  +handleSignout(): void
  -switchPage(t: Node, m: HBox): void
  -setMenu(a: HBox): void
  +update(): void
  +getMainContentPane(): Pane
  +getCurrentNode(): Node
  +setMainContentNode(n: Node): void
  +refreshSidebarFromSession(): void
  +applySearchFilter(k: String, c: String, min: double, max: double): void
  +updateRealtimeUi(ans: Item): void
  +getSearchKeyword(): String
  +getCategoryFilter(): String
  +getMinPrice(): double
  +getMaxPrice(): double
  +returnFromAddLot(r: boolean): void
  +showUserProfile(user: User): void
  +returnToAuction(): void
}

class AdminDashboardController {
  -usertable: TableView~User~
  -colusername: TableColumn~User, String~
  -colemail: TableColumn~User, String~
  -colrole: TableColumn~User, String~
  -colstatus: TableColumn~User, String~
  -colrating: TableColumn~User, String~
  -btnban: Button
  -btnunban: Button
  -pendingtable: TableView~Item~
  -colitemname: TableColumn~Item, String~
  -colitemseller: TableColumn~Item, String~
  -colitemprice: TableColumn~Item, String~
  -colitemcategory: TableColumn~Item, String~
  -btnapprove: Button
  -btnreject: Button
  -ratingfilter: ComboBox~String~
  -statuschart: PieChart
  -categorychart: BarChart~String, Number~
  -userlist: ObservableList~User~
  -filtereduserlist: FilteredList~User~
  -pendinglist: ObservableList~Item~
  +initialize(): void
  -loadUsers(): void
  -loadPendingItems(): void
  -loadStats(): void
  -handleBan(event: ActionEvent): void
  -handleUnban(event: ActionEvent): void
  -handlePromoteAdmin(event: ActionEvent): void
  -handleApprove(event: ActionEvent): void
  -handleReject(event: ActionEvent): void
  -handleFilterChange(event: ActionEvent): void
  -handleRefreshPending(event: ActionEvent): void
  -showAlert(type: AlertType, title: String, content: String): void
}
```

---

## 10) Client Module - `TrangChu` + `ItemCard`

```mermaid
classDiagram
direction LR

class TrangChuController {
  -instance: TrangChuController
  -TrendingBind: HBox
  -cacheditems: List~Lot~
  -cardmap: Map~Integer, ItemCardController~
  -kw: String
  -cat: String
  +getInstance(): TrangChuController
  ~initialize(): void
  +refreshItems(): void
  +setFilters(res: String, ans: String): void
  -cacheAndRender(res: List): void
  -renderFilteredItems(): void
  +updatePriceUi(ans: Item): void
  +updateItemPrice(ans: Item): void
  -match(ans: Lot): boolean
  -safe(ans: String): String
  -formatTime(ans: LocalDateTime): String
}

class ItemCardController {
  -itemRoot: VBox
  -ItemName: Label
  -ItemDescription: Label
  -Price: Label
  -TimeRemain: Label
  -ImageHolder: ImageView
  -id: int
  -n: String
  -d: String
  -t: String
  -u: String
  -sn: String
  -sa: String
  -p: double
  +setData(iid: int, iname: String, ip: double, idesc: String, it: String, iurl: String, isn: String, isa: String): void
  -applyCenterCrop(iv: ImageView, img: Image): void
  +updatePrice(res: double): void
  +getId(): int
  +handleItemClicked(): void
}
```

---

## 11) Client Module - `ItemInformation` + `BiddingForm` + `RatingForm`

```mermaid
classDiagram
direction LR

class ItemInformationController {
  -ItemImageHolder: ImageView
  -ItemName: Label
  -ItemDescription: Label
  -CurrentHighestBidValue: Label
  -MaxPriceValue: Label
  -EndsInValue: Label
  -SellerAvatar: ImageView
  -SellerName: Label
  -BidButton: Button
  -RateButton: Button
  -RatingsContainer: VBox
  -RatingFilterCombo: ComboBox~String~
  -autobidfield: TextField
  -autobidbutton: Button
  -pricechart: LineChart~String, Number~
  -id: int
  -n: String
  -currentMaxPrice: double
  -sellerId: int
  -winnerId: int
  -cachedratings: List~Rating~
  -ans1: XYChartSeries~String, Number~
  +setData(res: int, ans: String, res1: double, ans2: double, res2: String, ans3: String, res3: String, ans4: String, res4: String): void
  +refresh(): void
  -loadBidHistory(): void
  -setupRatingUi(res: Item): void
  -loadRatings(): void
  -handleRatingFilter(): void
  -renderRatings(res: String): void
  -showBiddingForm(): void
  -showRatingForm(): void
  -handleAutoBid(): void
  +getId(): int
  +updatePriceUi(res: Item): void
  -applyPriceFromItem(res: Item): void
  -appendPriceToChart(price: double): void
  +updateCurrentBid(val: double): void
  +markAsSold(): void
}

class BiddingFormController {
  -RootPane: Pane
  -ItemId: Label
  -ItemName: Label
  -MaxPriceInfo: Label
  -BidAmount: TextField
  -itemId: int
  -parent: ItemInformationController
  -removeForm(): void
  +setData(itemId: int, itemname: String, maxPrice: double): void
  +setParentController(p: ItemInformationController): void
  -handleConfirmBidding(): void
  -showAlert(type: AlertType, title: String, content: String): void
}

class RatingFormController {
  -RootPane: VBox
  -TitleLabel: Label
  -StarContainer: HBox
  -FeedbackField: TextArea
  -itemId: int
  -selectedStars: int
  -starLabels: LabelArray
  -onComplete: Runnable
  +initialize(): void
  +setData(itemId: int): void
  +setOnComplete(r: Runnable): void
  -selectStars(count: int): void
  -handleCancel(): void
  -handleSubmit(): void
  -showAlert(type: AlertType, title: String, content: String): void
}
```

---

## 12) Client Module - `SearchBar`, `History`, `YourItem`, `UserProfile`, `Profile`, `TransactionHistory`, `util`

```mermaid
classDiagram
direction LR

class ThanhTimKiemController {
  -searchField: TextField
  -categoryFilter: ComboBox~String~
  -bellButton: Button
  -itemsToggle: ToggleButton
  -usersToggle: ToggleButton
  -searchModeGroup: ToggleGroup
  -minpricefield: TextField
  -maxpricefield: TextField
  -filterButton: Button
  -ans: NotificationPopup
  -res: Timer
  -ans1: boolean
  -res1: Popup
  -ans2: VBox
  +initialize(): void
  +onSearchModeChanged(): void
  -debounceUserSearch(ans3: String): void
  -searchUsers(ans3: String): void
  -showUserResults(ans3: List~User~): void
  -buildUserRow(ans3: User): HBox
  -hideUserResults(): void
  +applyFilter(): void
  +toggleNotifications(): void
}

class HistoryController {
  -ongoingcontainer: FlowPane
  -upcomingcontainer: FlowPane
  -closedcontainer: FlowPane
  -pastcontainer: FlowPane
  +initialize(): void
  +refreshHistory(): void
  -fetchOngoing(id: int): List~Lot~
  -fetchUpcoming(id: int): List~Lot~
  -fetchClosed(id: int): List~Lot~
  -fetchPast(id: int): List~Lot~
  -renderCards(p: FlowPane, list: List~Lot~, isOngoing: boolean): void
  -safe(s: String): String
  -formatTime(t: LocalDateTime): String
}

class YourItemController {
  -ItemContainer: FlowPane
  -ActiveItemsValue: Label
  -InventoryValue: Label
  ~initialize(): void
  +refreshItems(): void
  -render(ans: List~Item~): void
  +setFilters(k: String, c: String): void
  -match(ans: Item): boolean
}

class UserProfileController {
  -avatarImageView: ImageView
  -usernameLabel: Label
  -fullNameLabel: Label
  -emailLabel: Label
  -ratingStarsLabel: Label
  -ratingCountLabel: Label
  -reputationWarning: Label
  -itemsBoughtLabel: Label
  -itemsSoldLabel: Label
  -roleLabel: Label
  -itemsContainer: FlowPane
  -targetUser: User
  +setUser(user: User): void
  -populateData(): void
  -loadAvatar(): void
  -loadSellerItems(): void
  -buildItemCard(item: Item): VBox
  +handleBack(): void
}

class ProfileController {
  -avatarimageview: ImageView
  -usernameLabel: Label
  -fullNameLabel: Label
  -emailLabel: Label
  -phoneLabel: Label
  -roleLabel: Label
  -balanceLabel: Label
  -moneySpentLabel: Label
  -itemsBoughtLabel: Label
  -moneyReceivedLabel: Label
  -itemsSoldLabel: Label
  -ratingStarsLabel: Label
  -ratingCountLabel: Label
  -reputationWarning: Label
  -verifiedLabel: Label
  -fullNameInput: TextField
  -emailInput: TextField
  -phoneInput: TextField
  -DepositAmountField: TextField
  -editButton: Button
  -toggleRoleButton: Button
  -bidderMetricsRow: HBox
  -sellerMetricsRow: HBox
  -editing: boolean
  -instance: ProfileController
  +getInstance(): ProfileController
  +initialize(): void
  +updateBalanceDirectly(u: User): void
  +handleDeposit(): void
  +handleToggleRole(): void
  +refreshData(): void
  -setEditingMode(v: boolean): void
  +handleEditProfile(): void
  +handleLogout(): void
  +handleChangeAvatar(): void
  +handleRefresh(event: ActionEvent): void
  +handleShowHistory(): void
}

class TransactionHistoryController {
  -table: TableView~TransactionLog~
  -idcol: TableColumn~TransactionLog, String~
  -typecol: TableColumn~TransactionLog, String~
  -amountcol: TableColumn~TransactionLog, String~
  -itemcol: TableColumn~TransactionLog, String~
  -datecol: TableColumn~TransactionLog, String~
  +initialize(): void
  -loadData(): void
}

class AddNewLotController {
  -productImageView: ImageView
  -lblStatus: Label
  -txtName: TextField
  -txtPrice: TextField
  -txtMaxPrice: TextField
  -txtQuantity: TextArea
  -startDatePicker: DatePicker
  -startHourCombo: ComboBox~Integer~
  -startMinuteCombo: ComboBox~Integer~
  -startSecondCombo: ComboBox~Integer~
  -endDatePicker: DatePicker
  -endHourCombo: ComboBox~Integer~
  -endMinuteCombo: ComboBox~Integer~
  -endSecondCombo: ComboBox~Integer~
  -classifyComboBox: ComboBox~String~
  -lotimageurl: String
  -fmt: DateTimeFormatter
  -uploadUiGen: AtomicLong
  -live: AddNewLotController
  -CATEGORY_IN_BOX: String
  -DEFAULT_CATEGORY: String
  +resetWhenOpening(): void
  +initialize(): void
  +handleChoosePicture(e: ActionEvent): void
  +handleSubmit(e: ActionEvent): void
  +handleCancel(e: ActionEvent): void
  -clearForm(): void
  -normalizeDateTimeForServer(date: LocalDate, hour: Integer, minute: Integer, second: Integer): String
  -parseClientDateTime(value: String): LocalDateTime
}

class NotificationCenter {
  -ans: ObservableList~String~
  +addNotification(res: String): void
  +getNotifications(): ObservableList~String~
}

class NotificationPopup {
  -ans: Popup
  +NotificationPopup()
  +show(res: Window, x: double, y: double): void
}

NotificationPopup ..> NotificationCenter
ThanhTimKiemController ..> NotificationPopup
```

