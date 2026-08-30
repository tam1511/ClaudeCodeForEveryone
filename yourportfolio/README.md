# Vibe Code Pro — Tài liệu tham khảo

Tài liệu đi kèm series video "Vibe Code Pro". Chứa toàn bộ link, lệnh cài đặt và file mẫu được nhắc đến trong video, để bạn không phải dừng video lại gõ theo.

Mọi lệnh trong file này đều đã được đối chiếu với tài liệu chính thức của Anthropic tại thời điểm viết. Công cụ thay đổi nhanh, nếu có gì lệch hãy kiểm tra lại tại [code.claude.com/docs](https://code.claude.com/docs/en/setup).

---

## Mục lục

1. [Yêu cầu hệ thống](#1-yêu-cầu-hệ-thống)
2. [Cài Git](#2-cài-git)
3. [Cài Node.js](#3-cài-nodejs)
4. [Cài VS Code](#4-cài-vs-code)
5. [Đăng ký gói Claude](#5-đăng-ký-gói-claude)
6. [Cài Claude Code](#6-cài-claude-code)
7. [Claude Code extension cho VS Code](#7-claude-code-extension-cho-vs-code)
8. [Cheat sheet lệnh và phím tắt](#8-cheat-sheet-lệnh-và-phím-tắt)
9. [OpenRouter và file .env](#10-openrouter-và-file-env)
10. [Phương án miễn phí](#11-phương-án-miễn-phí)
---

## 1. Yêu cầu hệ thống

Claude Code chạy trên:

| Hạng mục | Yêu cầu |
|---|---|
| macOS | 13.0 trở lên |
| Windows | Windows 10 phiên bản 1809 trở lên |
| Linux | Ubuntu 20.04+, Debian 10+, Alpine 3.19+ |
| Phần cứng | RAM từ 4 GB, CPU x64 hoặc ARM64 |
| Mạng | Bắt buộc có kết nối internet |
| Shell | Bash, Zsh, PowerShell hoặc CMD |
| Khu vực | Phải nằm trong [danh sách quốc gia được hỗ trợ](https://www.anthropic.com/supported-countries) |

---

## 2. Cài Git

Trang tải: **https://git-scm.com/downloads**

Kiểm tra đã có hay chưa:

```bash
git --version
```

Nếu hiện ra số phiên bản là xong. Nếu báo `command not found` thì vào link trên tải về và cài theo mặc định.

- macOS: có thể cài nhanh bằng `brew install git`, hoặc chạy `xcode-select --install`
- Windows: tải [Git for Windows](https://git-scm.com/downloads/win). Cài cái này còn có thêm lợi ích là Claude Code sẽ dùng được Git Bash thay vì PowerShell khi chạy lệnh shell.

Cấu hình lần đầu (bắt buộc nếu muốn commit):

```bash
git config --global user.name "Tên của bạn"
git config --global user.email "email@cua-ban.com"
```

---

## 3. Cài Node.js

Trang tải: **https://nodejs.org/en/download**

```bash
node --version
npm --version
```

Nên dùng bản LTS. Nếu bạn làm việc với nhiều dự án và cần đổi phiên bản Node qua lại, cân nhắc dùng [nvm](https://github.com/nvm-sh/nvm) (macOS/Linux) hoặc [nvm-windows](https://github.com/coreybutler/nvm-windows).

---

## 4. Cài VS Code

Trang tải: **https://code.visualstudio.com/**

Nút Download tự nhận diện hệ điều hành của bạn. Cài theo mặc định.

Mở terminal trong VS Code: `Ctrl + J` (Windows) hoặc `Cmd + J` (Mac), hoặc menu **View → Terminal**.

Nếu bạn quen dùng Cursor, Antigravity hay JetBrains thì cứ dùng, mọi thứ trong series này không phụ thuộc vào IDE.

---

## 5. Đăng ký gói Claude

Trang giá: **https://claude.com/pricing**

Claude Code **không có trong gói Free**. Bạn cần một trong các gói sau:

| Gói | Giá tham khảo | Ghi chú |
|---|---|---|
| Free | 0 | Chỉ chat trên web, **không có Claude Code** |
| Pro | 20 USD/tháng, 17 USD/tháng nếu trả theo năm | Đủ cho toàn bộ series này |
| Max 5x | từ 100 USD/tháng | Cho người dùng Claude Code cả ngày |
| Max 20x | 200 USD/tháng | Chạy nhiều agent song song |

Ngoài ra có thể dùng API key trả theo token qua [Claude Console](https://console.anthropic.com), hoặc qua Amazon Bedrock / Google Cloud / Microsoft Foundry.

Giá và hạn mức do Anthropic quyết định và có thể thay đổi — luôn kiểm tra lại tại trang pricing trước khi thanh toán.

**Phân biệt hai loại chi phí:**
- *Gói thuê bao* (Pro/Max): trả cố định hàng tháng, dùng Claude Code và Claude chat chung một hạn mức.
- *API cost*: tính theo token mỗi lần ứng dụng gọi model. Đây là loại chi phí mà **dự án portfolio ở phần sau sẽ phát sinh** khi khung chat gọi model qua OpenRouter (nếu bạn chọn model trả phí) — nó tách biệt hoàn toàn với gói Pro của bạn.

---

## 6. Cài Claude Code

Trang chủ: **https://code.claude.com** — Tài liệu: **https://code.claude.com/docs/en/setup**

### Cách 1 — Native installer (khuyến nghị)

**macOS, Linux, WSL:**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows PowerShell:**
```powershell
irm https://claude.ai/install.ps1 | iex
```

**Windows CMD:**
```batch
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

> Nếu gặp lỗi `The token '&&' is not a valid statement separator` nghĩa là bạn đang ở PowerShell chứ không phải CMD. Nếu gặp `'irm' is not recognized` thì ngược lại. Dấu nhận biết: PowerShell hiện `PS C:\`, CMD hiện `C:\`.

Bản native **tự động cập nhật ngầm**.

### Cách 2 — Homebrew (macOS/Linux)

```bash
brew install --cask claude-code
```

Không tự cập nhật. Nâng cấp bằng `brew upgrade claude-code`.

### Cách 3 — WinGet (Windows)

```powershell
winget install Anthropic.ClaudeCode
```

Không tự cập nhật. Nâng cấp bằng `winget upgrade Anthropic.ClaudeCode`.

### Cách 4 — npm

```bash
npm install -g @anthropic-ai/claude-code
```

Yêu cầu Node.js 22 trở lên. **Tuyệt đối không dùng `sudo npm install -g`** — sẽ gây lỗi quyền về sau.

### Kiểm tra sau khi cài

```bash
claude --version    # in ra số phiên bản, ví dụ 2.1.211 (Claude Code)
claude doctor       # kiểm tra sức khoẻ cài đặt và file settings
```

### Đăng nhập

Mở terminal trong thư mục dự án rồi gõ:

```bash
claude
```

Lần đầu chạy, Claude Code sẽ mở trình duyệt để bạn đăng nhập. Sau đó quay lại terminal là đã xác thực xong. Trong phiên làm việc, lệnh `/login` cũng làm việc tương tự.

### Cập nhật thủ công

```bash
claude update
```

---

## 7. Claude Code extension cho VS Code

Tài liệu: **https://code.claude.com/docs/en/vs-code**

Mở **View → Extensions** (`Cmd + Shift + X` / `Ctrl + Shift + X`), tìm "Claude Code", nhấn Install.

**So sánh nhanh hai cách dùng:**

| | Extension (sidebar) | CLI (terminal) |
|---|---|---|
| Trải nghiệm | Giống chat panel quen thuộc | Toàn bộ giao diện dòng lệnh |
| Tích hợp IDE | Sâu hơn — xem diff, chia sẻ selection | Vẫn có nếu chạy terminal trong VS Code |
| Tính năng | Là một tập con | Đầy đủ |
| Phù hợp | Người mới | Series này |

Series này dùng **CLI trong terminal của VS Code**, vì đó là bản đầy đủ tính năng nhất.

---

## 8. Cheat sheet lệnh và phím tắt

### Slash command

| Lệnh | Công dụng |
|---|---|
| `/help` | Tóm tắt các lệnh và phím tắt quan trọng |
| `/login` | Đăng nhập tài khoản Anthropic |
| `/init` | Quét dự án và tự sinh `CLAUDE.md`. Hữu ích với dự án có sẵn |
| `/model` | Xem và đổi model đang dùng |
| `/context` | Xem context window đang bị tiêu thụ ra sao |
| `/compact` | Nén lịch sử hội thoại thành bản tóm tắt |
| `/clear` | Xoá sạch lịch sử, bắt đầu lại như session mới |
| `/permissions` | Xem và sửa các rule quyền đã cấp |

Gõ `/` rồi nhấn mũi tên xuống để xem toàn bộ danh sách kèm mô tả.

### Phím tắt

| Phím | Công dụng |
|---|---|
| `Shift + Tab` | Xoay vòng qua các permission mode, trong đó có **Plan mode** |
| `Ctrl + O` | Bật/tắt transcript chi tiết, xem agent đang làm gì |
| `Ctrl + C` (2 lần) | Thoát Claude Code |

### Ba permission mode

1. **Default** — hỏi trước mỗi lần sửa file
2. **Accept edits** — tự động chấp nhận chỉnh sửa, chạy liền mạch
3. **Plan mode** — chỉ đọc. Agent được đọc, tìm kiếm, phân tích nhưng **không sửa gì** cho tới khi bạn duyệt kế hoạch. Đây là chỗ rẻ nhất để phát hiện agent hiểu sai đề bài.

### Quy tắc khi Claude xin quyền

Khi hiện menu đánh số:
- Chọn **2** cho những thao tác bạn hiểu và sẽ lặp lại nhiều lần (chạy test, cài thư viện). Mỗi lần chọn 2, một rule được ghi vào thư mục `.claude/` và sống lâu hơn phiên làm việc.
- Chọn **1** cho những thao tác cần cân nhắc từng lần, đặc biệt là bất cứ thứ gì chạm ra ngoài thư mục dự án.
- **Không hiểu lệnh đang được xin phép thì đừng nhấn bừa.** Từ chối rồi hỏi thẳng Claude: "Command này làm gì và tại sao cần nó?"

### Ba cơ chế quay lại — đừng nhầm lẫn

| Cơ chế | Khôi phục cái gì | Dùng khi nào |
|---|---|---|
| **Session** | Lịch sử hội thoại và context | Tiếp tục công việc hôm qua |
| **Checkpoint** | Những thay đổi Claude tự thực hiện và theo dõi được. **Không phải bản chụp toàn bộ dự án** | Rewind nhanh ngay sau một thay đổi hỏng |
| **Git** | Trạng thái toàn bộ file được Git theo dõi | Quản lý lịch sử code lâu dài |

Nguyên tắc xuyên suốt series: **commit sau mỗi phase**. Đừng bao giờ tin tưởng hoàn toàn vào agent cho tới khi code đã được commit.

---

## 9. OpenRouter và file .env

OpenRouter là nơi bạn gọi tới gần như mọi model, cả trả phí lẫn miễn phí, qua một API key duy nhất.

1. Truy cập **https://openrouter.ai** và đăng ký (đăng nhập bằng Google được).
2. Vào **Keys → Create Key**, sao chép key.
3. Tạo file `.env` ở thư mục gốc dự án:

```
OPENROUTER_API_KEY=sk-or-v1-...
OWNER_USER=ten-dang-nhap-cua-ban
OWNER_PASSWORD=mat-khau-manh-cua-ban
AI_MODEL=...
```

4. **Kiểm tra `.gitignore` đã có dòng `.env`** trước khi commit lần đầu. Đây là bước không được phép sai.

**Chọn model:** model bạn chọn **bắt buộc phải hỗ trợ tool calling / function calling**, vì toàn bộ tính năng thao tác qua chat ở Phase 10 dựa trên đó. Vào trang model trên OpenRouter kiểm tra phần Supported Parameters trước khi dùng. Model miễn phí thường có hậu tố `:free` trong tên và bị giới hạn tần suất khá chặt.

**Nếu đã lỡ commit `.env` lên GitHub:** coi như key đã lộ. Vào OpenRouter thu hồi key cũ và tạo key mới ngay, sau đó mới xử lý phần lịch sử Git. Xoá file rồi commit lại là không đủ, key vẫn nằm trong lịch sử.

---

## 10. Phương án miễn phí

Nếu chưa muốn trả 20 USD/tháng, có mấy hướng thay thế.

### OpenCode

**https://opencode.ai** — đối thủ mã nguồn mở của Claude Code, kết nối được với gần như mọi nhà cung cấp.

```bash
opencode          # khởi động trong thư mục dự án
/models           # đổi model
/connect          # kết nối nhà cung cấp: OpenAI, Anthropic, OpenRouter, Ollama...
```

Nhấn `Tab` để chuyển giữa chế độ plan và build. Toàn bộ nội dung series này bạn có thể thực hành bằng OpenCode nếu muốn.

### AMP Code

**https://ampcode.com** — chương trình AMP Free cấp credit dùng model mỗi ngày để đổi lấy việc xem quảng cáo. AMP tự chọn model phía sau thay vì để bạn chọn. `Ctrl + S` đổi giữa các chế độ `smart` / `deep` / `rush`.

### Claude Code trỏ sang nhà cung cấp khác

Cách này **không phải cách Anthropic khuyến nghị** — Claude Code được tối ưu quanh model của Anthropic, dùng model khác có thể gặp trục trặc về tooling. Chỉ thử nếu bạn muốn tìm hiểu sâu. Nếu mục tiêu chỉ là dùng model open-source thì OpenCode hoặc AMP là lựa chọn tốt hơn.

Nguyên lý: trỏ `ANTHROPIC_BASE_URL` sang endpoint khác và dùng `ANTHROPIC_AUTH_TOKEN` thay cho key của Anthropic.

```bash
# Ví dụ trỏ sang OpenRouter (macOS/Linux)
export ANTHROPIC_BASE_URL=https://openrouter.ai/api
export ANTHROPIC_AUTH_TOKEN=$OPENROUTER_API_KEY
unset ANTHROPIC_API_KEY

claude --model <ten-model-tren-openrouter>
```

Nhớ trỏ cả `ANTHROPIC_DEFAULT_SONNET_MODEL` và `ANTHROPIC_DEFAULT_OPUS_MODEL` về cùng model đó, nếu không Claude Code có thể tự chuyển về model Claude.

Kiểm chứng nó thật sự đang gọi OpenRouter: mở trang **Activity** trên OpenRouter xem request gần nhất.

### Ollama chạy local

**https://ollama.com** — chạy model ngay trên máy, không tốn một đồng nào. Ollama mặc định chạy ở `localhost:11434`.

Cần một máy đủ mạnh. Với model lớn, GPU sẽ chạy gần hết công suất. Nếu mục tiêu là dùng model thật mạnh thì OpenRouter thường vẫn hợp lý hơn về chi phí so với đầu tư phần cứng.

Đóng terminal và mở terminal mới là các biến môi trường tạm sẽ reset, Claude Code quay về dùng Claude bình thường.

---

