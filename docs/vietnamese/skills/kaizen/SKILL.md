---
name: kaizen
description: Hướng dẫn cải tiến liên tục, chống lỗi và chuẩn hóa. Sử dụng kỹ năng này khi người dùng muốn cải thiện chất lượng code, tái cấu trúc (refactor) hoặc thảo luận về cải tiến quy trình.
---

# Kaizen: Cải tiến Liên tục

## Tổng quan

Những cải tiến nhỏ, diễn ra liên tục. Thiết kế để chống lỗi (Error-proof). Tuân theo những gì hiệu quả. Chỉ xây dựng những gì cần thiết.

**Nguyên tắc cốt lõi:** Nhiều cải tiến nhỏ đánh bại một thay đổi lớn. Ngăn chặn lỗi ngay từ lúc thiết kế, không phải bằng các bản vá.

## Khi nào nên Sử dụng

**Luôn áp dụng cho:**

- Triển khai và tái cấu trúc code
- Các quyết định về kiến trúc và thiết kế
- Cải thiện quy trình và luồng công việc
- Xử lý lỗi và xác thực (validation)

**Triết lý:** Chất lượng đến từ sự tiến bộ từng bước và sự ngăn ngừa, không phải sự hoàn hảo thông qua nỗ lực khổng lồ.

## Bốn Trụ cột

### 1. Cải tiến Liên tục (Kaizen)

Những cải tiến nhỏ, thường xuyên sẽ tích lũy thành những thành quả lớn.

#### Nguyên tắc

**Gia tăng (Incremental) hơn là Cách mạng:**

- Thực hiện thay đổi nhỏ nhất có thể nhưng cải thiện được chất lượng
- Một cải tiến tại một thời điểm
- Xác minh từng thay đổi trước khi sang bước tiếp theo
- Xây dựng đà phát triển thông qua những thắng lợi nhỏ

**Luôn để lại code tốt hơn lúc đầu:**

- Sửa các vấn đề nhỏ ngay khi bạn gặp chúng
- Refactor trong khi làm việc (trong phạm vi cho phép)
- Cập nhật các comment lỗi thời
- Xóa code chết (dead code) khi bạn thấy nó

**Tinh chỉnh lặp lại (Iterative refinement):**

- Phiên bản đầu tiên: làm cho nó hoạt động (work)
- Phiên bản thứ hai: làm cho nó rõ ràng (clear)
- Phiên bản thứ ba: làm cho nó hiệu quả (efficient)
- Đừng cố gắng làm cả ba cùng một lúc

<Good>
```typescript
// Lần lặp 1: Làm cho nó hoạt động
const calculateTotal = (items: Item[]) => {
  let total = 0;
  for (let i = 0; i < items.length; i++) {
    total += items[i].price * items[i].quantity;
  }
  return total;
};

// Lần lặp 2: Làm cho nó rõ ràng (refactor)
const calculateTotal = (items: Item[]): number => {
  return items.reduce((total, item) => {
    return total + (item.price * item.quantity);
  }, 0);
};

// Lần lặp 3: Làm cho nó mạnh mẽ (thêm validation)
const calculateTotal = (items: Item[]): number => {
  if (!items?.length) return 0;

  return items.reduce((total, item) => {
    if (item.price < 0 || item.quantity < 0) {
      throw new Error('Price and quantity must be non-negative');
    }
    return total + (item.price * item.quantity);
  }, 0);
};
```
Mỗi bước đều hoàn chỉnh, đã được kiểm thử và hoạt động tốt
</Good>

<Bad>
```typescript
// Cố gắng làm mọi thứ cùng một lúc
const calculateTotal = (items: Item[]): number => {
  // Validate, tối ưu hóa, thêm tính năng, xử lý trường hợp biên cùng lúc
  if (!items?.length) return 0;
  const validItems = items.filter(item => {
    if (item.price < 0) throw new Error('Negative price');
    if (item.quantity < 0) throw new Error('Negative quantity');
    return item.quantity > 0; // Cũng lọc luôn số lượng bằng 0
  });
  // Cộng thêm caching, logging, chuyển đổi tiền tệ...
  return validItems.reduce(...); // Quá nhiều mối quan tâm cùng lúc
};
```
Choáng ngợp, dễ lỗi, khó xác minh
</Bad>

#### Trong Thực tế

**Khi triển khai tính năng:**

1. Bắt đầu với phiên bản đơn giản nhất có thể hoạt động
2. Thêm một cải tiến (xử lý lỗi, validation, v.v.)
3. Kiểm thử và xác minh
4. Lặp lại nếu thời gian cho phép
5. Đừng cố làm cho nó hoàn hảo ngay lập tức

**Khi tái cấu trúc (refactoring):**

- Sửa từng vấn đề (code smell) một
- Commit sau mỗi cải tiến
- Giữ cho các bài kiểm tra luôn xanh (pass) trong suốt quá trình
- Dừng lại khi "đủ tốt" (hiệu suất giảm dần)

**Khi review code:**

- Đề xuất các cải tiến nhỏ (không phải viết lại toàn bộ)
- Ưu tiên: tối quan trọng → quan trọng → có thì tốt (nice-to-have)
- Tập trung vào những thay đổi có tác động lớn nhất trước
- Chấp nhận "tốt hơn trước đó" ngay cả khi chưa hoàn hảo

### 2. Poka-Yoke (Chống lỗi)

Thiết kế hệ thống ngăn chặn lỗi tại thời điểm biên dịch/thiết kế, không phải tại thời điểm chạy (runtime).

#### Nguyên tắc

**Làm cho lỗi không thể xảy ra:**

- Hệ thống Type bắt các sai sót
- Trình biên dịch thực thi các hợp đồng (contracts)
- Các trạng thái không hợp lệ không thể biểu diễn được
- Lỗi được bắt sớm (dịch chuyển sang trái quy trình sản xuất - left of production)

**Thiết kế để an toàn:**

- Thất bại nhanh và rõ ràng (Fail fast and loudly)
- Cung cấp thông báo lỗi hữu ích
- Làm cho con đường đúng đắn trở nên rõ ràng
- Làm cho con đường sai trở nên khó khăn

**Phòng thủ theo lớp:**

1. Hệ thống Type (thời điểm biên dịch)
2. Validation (thời điểm chạy, sớm)
3. Guards (điều kiện tiên quyết)
4. Ranh giới lỗi (xuống cấp nhẹ nhàng - graceful degradation)

#### Chống lỗi bằng Hệ thống Type

<Good>
```typescript
// Lỗi: trạng thái dạng string có thể là bất kỳ giá trị nào
type OrderBad = {
  status: string; // Có thể là "pending", "PENDING", "pnding", bất cứ thứ gì!
  total: number;
};

// Tốt: Chỉ các trạng thái hợp lệ mới khả thi
type OrderStatus = 'pending' | 'processing' | 'shipped' | 'delivered';
type Order = {
  status: OrderStatus;
  total: number;
};

// Tốt hơn: Trạng thái đi kèm dữ liệu liên quan
type Order =
  | { status: 'pending'; createdAt: Date }
  | { status: 'processing'; startedAt: Date; estimatedCompletion: Date }
  | { status: 'shipped'; trackingNumber: string; shippedAt: Date }
  | { status: 'delivered'; deliveredAt: Date; signature: string };

// Giờ đây không thể có trạng thái 'shipped' mà thiếu 'trackingNumber'
```
Hệ thống Type ngăn chặn toàn bộ các lớp lỗi
</Good>

<Good>
```typescript
// Làm cho trạng thái không hợp lệ không thể biểu diễn
type NonEmptyArray<T> = [T, ...T[]];

const firstItem = <T>(items: NonEmptyArray<T>): T => {
  return items[0]; // Luôn an toàn, không bao giờ undefined!
};

// Người gọi phải chứng minh mảng không rỗng
const items: number[] = [1, 2, 3];
if (items.length > 0) {
  firstItem(items as NonEmptyArray<number>); // An toàn
}
```
Chữ ký hàm đảm bảo an toàn
</Good>

#### Chống lỗi bằng Validation

<Good>
```typescript
// Lỗi: Validation sau khi sử dụng
const processPayment = (amount: number) => {
  const fee = amount * 0.03; // Đã dùng trước khi validate!
  if (amount <= 0) throw new Error('Invalid amount');
  // ...
};

// Tốt: Validate ngay lập tức
const processPayment = (amount: number) => {
  if (amount <= 0) {
    throw new Error('Payment amount must be positive');
  }
  if (amount > 10000) {
    throw new Error('Payment exceeds maximum allowed');
  }

  const fee = amount * 0.03;
  // ... giờ đã an toàn để sử dụng
};

// Tốt hơn: Validate tại ranh giới với branded type
type PositiveNumber = number & { readonly __brand: 'PositiveNumber' };

const validatePositive = (n: number): PositiveNumber => {
  if (n <= 0) throw new Error('Must be positive');
  return n as PositiveNumber;
};

const processPayment = (amount: PositiveNumber) => {
  // amount được đảm bảo là số dương, không cần kiểm tra lại
  const fee = amount * 0.03;
};

// Validate tại ranh giới hệ thống
const handlePaymentRequest = (req: Request) => {
  const amount = validatePositive(req.body.amount); // Validate một lần
  processPayment(amount); // Sử dụng mọi nơi an toàn
};
```
Validate một lần tại ranh giới, an toàn ở mọi nơi khác
</Good>

#### Guards và Điều kiện tiên quyết

<Good>
```typescript
// Return sớm ngăn chặn code lồng nhau sâu
const processUser = (user: User | null) => {
  if (!user) {
    logger.error('User not found');
    return;
  }

  if (!user.email) {
    logger.error('User email missing');
    return;
  }

  if (!user.isActive) {
    logger.info('User inactive, skipping');
    return;
  }

  // Logic chính ở đây, đảm bảo user hợp lệ và đang hoạt động
  sendEmail(user.email, 'Welcome!');
};
```
Guards làm cho các giả định trở nên rõ ràng và được thực thi
</Good>

#### Chống lỗi Cấu hình

<Good>
```typescript
// Lỗi: Cấu hình tùy chọn với mặc định không an toàn
type ConfigBad = {
  apiKey?: string;
  timeout?: number;
};

const client = new APIClient({ timeout: 5000 }); // Thiếu apiKey!

// Tốt: Cấu hình bắt buộc, lỗi sớm
type Config = {
  apiKey: string;
  timeout: number;
};

const loadConfig = (): Config => {
  const apiKey = process.env.API_KEY;
  if (!apiKey) {
    throw new Error('API_KEY environment variable required');
  }

  return {
    apiKey,
    timeout: 5000,
  };
};

// App lỗi ngay khi khởi động nếu config không hợp lệ, không phải lúc đang request
const config = loadConfig();
const client = new APIClient(config);
```
Lỗi lúc khởi động, không phải trong môi trường producton
</Good>

#### Trong Thực tế

**Khi thiết kế API:**
- Sử dụng Types để ràng buộc đầu vào
- Làm cho trạng thái không hợp lệ không thể biểu diễn
- Trả về Result<T, E> thay vì ném ra lỗi (throwing)
- Tài liệu hóa các điều kiện tiên quyết trong Types

**Khi xử lý lỗi:**
- Validate tại ranh giới hệ thống
- Sử dụng guards cho điều kiện tiên quyết
- Lỗi nhanh với thông báo rõ ràng
- Log ngữ cảnh để debug

**Khi cấu hình:**
- Ưu tiên bắt buộc hơn là tùy chọn có mặc định
- Validate tất cả config lúc khởi động
- Làm thất bại việc triển khai nếu config không hợp lệ
- Không cho phép cấu hình một phần

### 3. Công việc Chuẩn hóa (Standardized Work)

Tuân theo các mẫu đã được thiết lập. Tài liệu hóa những gì hiệu quả. Làm cho các thực hành tốt trở nên dễ dàng tuân theo.

#### Nguyên tắc

**Nhất quán hơn là Thông minh:**
- Tuân theo các mẫu của codebase hiện có
- Đừng phát minh lại những vấn đề đã được giải quyết
- Mẫu mới chỉ được dùng nếu tốt hơn đáng kể
- Sự đồng thuận của nhóm về các mẫu mới

**Tài liệu sống cùng code:**
- README cho thiết lập và kiến trúc
- CLAUDE.md cho quy ước lập trình AI
- Comment giải thích "tại sao", không phải "cái gì"
- Ví dụ cho các mẫu phức tạp

**Tự động hóa các tiêu chuẩn:**
- Linters thực thi phong cách (style)
- Type checks thực thi hợp đồng
- Tests xác minh hành vi
- CI/CD thực thi các cổng kiểm soát chất lượng (quality gates)

#### Tuân theo các Mẫu (Patterns)

<Good>
```typescript
// Mẫu codebase hiện tại cho API clients
class UserAPIClient {
  async getUser(id: string): Promise<User> {
    return this.fetch(`/users/${id}`);
  }
}

// Code mới tuân theo cùng một mẫu
class OrderAPIClient {
  async getOrder(id: string): Promise<Order> {
    return this.fetch(`/orders/${id}`);
  }
}
```
Sự nhất quán làm cho codebase dễ dự đoán
</Good>

<Bad>
```typescript
// Mẫu hiện tại sử dụng class
class UserAPIClient { /* ... */ }

// Code mới giới thiệu mẫu khác mà không thảo luận
const getOrder = async (id: string): Promise<Order> => {
  // Phá vỡ sự nhất quán "vì tôi thích dùng hàm hơn"
};
```
Sự không nhất quán tạo ra sự nhầm lẫn
</Bad>

#### Các Mẫu Xử lý Lỗi

<Good>
```typescript
// Tiêu chuẩn dự án: Kiểu Result cho các lỗi có thể phục hồi
type Result<T, E> = { ok: true; value: T } | { ok: false; error: E };

// Tất cả service tuân theo mẫu này
const fetchUser = async (id: string): Promise<Result<User, Error>> => {
  try {
    const user = await db.users.findById(id);
    if (!user) {
      return { ok: false, error: new Error('User not found') };
    }
    return { ok: true, value: user };
  } catch (err) {
    return { ok: false, error: err as Error };
  }
};

// Người gọi sử dụng mẫu nhất quán
const result = await fetchUser('123');
if (!result.ok) {
  logger.error('Failed to fetch user', result.error);
  return;
}
const user = result.value; // Type-safe!
```
Mẫu tiêu chuẩn trên toàn bộ codebase
</Good>

#### Tiêu chuẩn Tài liệu

<Good>
```typescript
/**
 * Thử lại một thao tác bất đồng bộ với exponential backoff.
 *
 * Why: Các yêu cầu mạng thất bại tạm thời; thử lại giúp cải thiện độ tin cậy
 * When to use: Gọi API bên ngoài, thao tác cơ sở dữ liệu
 * When not to use: Validation đầu vào người dùng, gọi hàm nội bộ
 *
 * @example
 * const result = await retry(
 *   () => fetch('https://api.example.com/data'),
 *   { maxAttempts: 3, baseDelay: 1000 }
 * );
 */
const retry = async <T>(
  operation: () => Promise<T>,
  options: RetryOptions
): Promise<T> => {
  // Implementation...
};
```
Tài liệu hóa tại sao, khi nào và làm thế nào
</Good>

#### Trong Thực tế

**Trước khi thêm mẫu mới:**
- Tìm kiếm trong codebase các vấn đề tương tự đã được giải quyết
- Kiểm tra CLAUDE.md cho các quy ước dự án
- Thảo luận với nhóm nếu phá vỡ mẫu cũ
- Cập nhật tài liệu khi giới thiệu mẫu mới

**Khi viết code:**
- Khớp với cấu trúc file hiện có
- Sử dụng cùng quy ước đặt tên
- Tuân theo cùng cách tiếp cận xử lý lỗi
- Import từ cùng vị trí

**Khi review:**
- Kiểm tra tính nhất quán với code hiện có
- Chỉ ra các ví dụ trong codebase
- Đề xuất căn chỉnh với các tiêu chuẩn
- Cập nhật CLAUDE.md nếu có tiêu chuẩn mới xuất hiện

### 4. Just-In-Time (JIT - Vừa đủ, Đúng lúc)

Xây dựng những gì cần thiết ngay bây giờ. Không hơn, không kém. Tránh tối ưu hóa sớm và kỹ thuật quá mức (over-engineering).

#### Nguyên tắc

**YAGNI (You Aren't Gonna Need It - Bạn sẽ không cần nó đâu):**
- Chỉ triển khai các yêu cầu hiện tại
- Không có tính năng "phòng khi cần"
- Không có code "chúng ta có thể cần cái này sau này"
- Xóa bỏ sự suy đoán

**Thứ đơn giản nhất có thể hoạt động:**
- Bắt đầu với giải pháp đơn giản, trực tiếp
- Chỉ thêm độ phức tạp khi cần thiết
- Refactor khi yêu cầu thay đổi
- Đừng đoán trước nhu cầu tương lai

**Tối ưu hóa khi đã đo lường:**
- Không tối ưu hóa sớm
- Đo đạc (profile) trước khi tối ưu
- Đo lường tác động của thay đổi
- Chấp nhận hiệu suất "đủ tốt"

#### YAGNI trong Hành động

<Good>
```typescript
// Yêu cầu hiện tại: Log lỗi ra console
const logError = (error: Error) => {
  console.error(error.message);
};
```
Đơn giản, đáp ứng nhu cầu hiện tại
</Good>

<Bad>
```typescript
// Kỹ thuật quá mức cho "nhu cầu tương lai"
interface LogTransport {
  write(level: LogLevel, message: string, meta?: LogMetadata): Promise<void>;
}

class ConsoleTransport implements LogTransport { /*... */ }
class FileTransport implements LogTransport { /* ... */ }
class RemoteTransport implements LogTransport { /* ...*/ }

class Logger {
  private transports: LogTransport[] = [];
  private queue: LogEntry[] = [];
  private rateLimiter: RateLimiter;
  private formatter: LogFormatter;

  // 200 dòng code cho "có lẽ chúng ta sẽ cần nó"
}

const logError = (error: Error) => {
  Logger.getInstance().log('error', error.message);
};
```
Xây dựng cho các yêu cầu tưởng tượng trong tương lai
</Bad>

**Khi nào nên thêm độ phức tạp:**
- Yêu cầu hiện tại đòi hỏi nó
- Điểm đau (pain points) được xác định qua quá trình sử dụng
- Các vấn đề hiệu suất đã được đo lường
- Nhiều trường hợp sử dụng xuất hiện

<Good>
```typescript
// Bắt đầu đơn giản
const formatCurrency = (amount: number): string => {
  return `$${amount.toFixed(2)}`;
};

// Yêu cầu phát triển: hỗ trợ nhiều loại tiền tệ
const formatCurrency = (amount: number, currency: string): string => {
  const symbols = { USD: '$', EUR: '€', GBP: '£' };
  return `${symbols[currency]}${amount.toFixed(2)}`;
};

// Yêu cầu phát triển: hỗ trợ bản địa hóa (localization)
const formatCurrency = (amount: number, locale: string): string => {
  return new Intl.NumberFormat(locale, {
    style: 'currency',
    currency: locale === 'en-US' ? 'USD' : 'EUR',
  }).format(amount);
};
```
Độ phức tạp chỉ được thêm vào khi cần
</Good>

#### Trừu tượng hóa Sớm (Premature Abstraction)

<Bad>
```typescript
// Một trường hợp sử dụng, nhưng xây dựng framework chung chung
abstract class BaseCRUDService<T> {
  abstract getAll(): Promise<T[]>;
  abstract getById(id: string): Promise<T>;
  abstract create(data: Partial<T>): Promise<T>;
  abstract update(id: string, data: Partial<T>): Promise<T>;
  abstract delete(id: string): Promise<void>;
}

class GenericRepository<T> { /* 300 dòng */ }
class QueryBuilder<T> { /* 200 dòng */ }
// ... xây dựng toàn bộ ORM cho một bảng duy nhất
```
Trừu tượng hóa khổng lồ cho tương lai không chắc chắn
</Bad>

<Good>
```typescript
// Các hàm đơn giản cho nhu cầu hiện tại
const getUsers = async (): Promise<User[]> => {
  return db.query('SELECT * FROM users');
};

const getUserById = async (id: string): Promise<User | null> => {
  return db.query('SELECT * FROM users WHERE id = $1', [id]);
};

// Khi mẫu xuất hiện trên nhiều thực thể, thì mới trừu tượng hóa
```
Chỉ trừu tượng hóa khi mẫu đã được chứng minh qua 3+ trường hợp
</Good>

#### Tối ưu hóa Hiệu suất

<Good>
```typescript
// Hiện tại: Tiếp cận đơn giản
const filterActiveUsers = (users: User[]): User[] => {
  return users.filter(user => user.isActive);
};

// Benchmark cho thấy: 50ms cho 1000 user (chấp nhận được)
// ✓ Ship nó, không cần tối ưu

// Sau này: Sau khi profiling cho thấy đây là nút thắt cổ chai
// Thì mới tối ưu với tìm kiếm index hoặc caching
```
Tối ưu hóa dựa trên đo lường, không phải giả định
</Good>

<Bad>
```typescript
// Tối ưu hóa sớm
const filterActiveUsers = (users: User[]): User[] => {
  // "Cái này có thể chậm, nên hãy cache và index"
  const cache = new WeakMap();
  const indexed = buildBTreeIndex(users, 'isActive');
  // 100 dòng code tối ưu
  // Thêm độ phức tạp, khó bảo trì hơn
  // Không có bằng chứng là nó cần thiết
};
```
Giải pháp phức tạp cho vấn đề chưa được đo lường
</Bad>

#### Trong Thực tế

**Khi triển khai:**
- Giải quyết vấn đề trước mắt
- Sử dụng cách tiếp cận thẳng thắn
- Chống lại suy nghĩ "nếu như" (what if)
- Xóa code suy đoán

**Khi tối ưu:**
- Profile trước, tối ưu sau
- Đo trước và sau
- Tài liệu hóa lý do cần tối ưu
- Giữ phiên bản đơn giản trong tests

**Khi trừu tượng hóa:**
- Đợi cho đến khi có 3+ trường hợp tương tự (Quy tắc số 3)
- Làm cho sự trừu tượng hóa đơn giản nhất có thể
- Thà lặp code còn hơn trừu tượng hóa sai
- Refactor khi mẫu đã rõ ràng

## Tích hợp với các Lệnh

Skill Kaizen hướng dẫn cách bạn làm việc. Các lệnh cung cấp phân tích có cấu trúc:

- **`/why`**: Phân tích nguyên nhân gốc rễ (5 Whys)
- **`/cause-and-effect`**: Phân tích đa yếu tố (Biểu đồ Xương cá)
- **`/plan-do-check-act`**: Các chu trình cải tiến lặp lại
- **`/analyse-problem`**: Tài liệu hóa toàn diện (A3)
- **`/analyse`**: Lựa chọn phương pháp thông minh (Gemba/VSM/Muda)

Sử dụng các lệnh cho việc giải quyết vấn đề có cấu trúc. Áp dụng skill cho việc phát triển hàng ngày.

## Cờ Đỏ (Red Flags)

**Vi phạm Cải tiến Liên tục:**
- "Tôi sẽ refactor nó sau" (không bao giờ xảy ra)
- Để lại code tệ hơn lúc bạn tìm thấy nó
- Viết lại kiểu "big bang" thay vì gia tăng từng chút một

**Vi phạm Poka-Yoke:**
- "Người dùng chỉ cần cẩn thận là được"
- Validation sau khi sử dụng thay vì trước đó
- Config tùy chọn mà không có validation

**Vi phạm Công việc Chuẩn hóa:**
- "Tôi thích làm theo cách của mình hơn"
- Không kiểm tra các mẫu hiện có
- Phớt lờ các quy ước dự án

**Vi phạm Just-In-Time:**
- "Chúng ta có thể cần cái này vào lúc nào đó"
- Xây dựng frameworks trước khi sử dụng chúng
- Tối ưu hóa mà không đo lường

## Hãy nhớ

**Kaizen là về:**
- Cải tiến nhỏ liên tục
- Ngăn ngừa lỗi bằng thiết kế
- Tuân theo các mẫu đã được kiểm chứng
- Chỉ xây dựng những gì cần thiết

**Không phải là về:**
- Hoàn hảo ngay lần thử đầu tiên
- Các dự án refactoring khổng lồ
- Các sự trừu tượng hóa thông minh (clever)
- Tối ưu hóa sớm

**Tư duy:** Đủ tốt cho hôm nay, tốt hơn vào ngày mai. Lặp lại.
