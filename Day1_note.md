# 🔐 資安之路 Day 1

## 1. ROT13

**ROT13** 是一種簡單的 substitution cipher（替換式密碼），會將每個英文字母往後移 **13 位**。

例如：

```text
A → N
B → O
N → A
```

因為英文字母有 26 個，所以 ROT13 執行兩次就會回到原文：

```text
ROT13(ROT13(text)) = text
```

### CTF 小技巧

如果看到：

```text
synt{...}
```

很有可能可以嘗試 ROT13，因為：

```text
synt → flag
```

所以：

```text
synt{...} → flag{...}
```

---

## 2. wget

`wget` 可以從指定的 URL 下載檔案。

```bash
wget <URL>
```

例如：

```bash
wget https://example.com/file.zip
```

預設會下載到目前所在的 directory。

可以使用：

```bash
wget --help
```

查看 `wget` 支援的參數。

> `<URL>` 中的 `< >` 通常代表「請替換成實際內容」，不是真的要輸入 `< >`。

---

## 3. chmod +x

如果下載的檔案沒有 executable（執行）權限，可以使用：

```bash
chmod +x filename
```

其中：

```text
chmod = change mode
+x    = 加上 executable 權限
```

接著可以：

```bash
./filename
```

執行目前 directory 中的檔案。

可以用：

```bash
ls -l filename
```

查看權限，例如：

```text
-rwxr-xr-x
```

其中：

```text
r = read
w = write
x = execute
```

---

## 4. Tab Completion

在 Terminal 裡面 **Tab 超級好用！**

輸入檔名或 directory 名稱的前幾個字母後按：

```text
Tab
```

Terminal 可以自動補完名稱。

例如有：

```text
super_long_challenge_filename
```

不用全部打完，可以輸入：

```bash
./super
```

然後按 `Tab` 自動補完。

尤其在處理很長的 directory path 或 filename 時很好用，也能降低打錯字的機率。

---

## 5. SSH

**SSH（Secure Shell）** 主要用來安全地登入並操作遠端 Server。

基本語法：

```bash
ssh <username>@<server-ip>
```

例如：

```bash
ssh gabe@192.168.1.10
```

登入成功後，就可以在遠端 Server 上執行：

```bash
ls
cd
pwd
cat
./program
```

重點：

```text
SSH = 遠端登入 + 加密連線 + 執行遠端指令
```

SSH 預設使用 **TCP port 22**。

---

## 6. Netcat（nc）

**Netcat (`nc`)** 是一個簡單但很強大的 networking tool，可以透過 **TCP / UDP 建立連線並收發資料**。

它常被用來：

- 測試某個 IP / Port 是否能連線
- 連接 CTF challenge server
- 建立簡單的 TCP / UDP client
- Listen（監聽）某個 port
- 手動傳送 / 接收資料

例如：

```bash
nc <server-ip> <port>
```

CTF 中可能會看到：

```bash
nc example.com 5000
```

代表：

```text
我的電腦 ──TCP──> example.com:5000
```

### Listen

也可以讓 `nc` 在某個 port 等待連線：

```bash
nc -l 5000
```

代表監聽 port `5000`。

---

## 7. SSH vs Netcat

兩個看起來都可以「連到 Server」，但用途不同：

| | SSH | Netcat (`nc`) |
|---|---|---|
| 主要用途 | 遠端登入 Server | 建立 TCP/UDP 連線、收發資料 |
| 遠端 Terminal | ✅ | ❌ 本身不是遠端 shell |
| 加密 | ✅ | ❌ 一般 nc 沒有 |
| Authentication | ✅ | ❌ |
| TCP | ✅ | ✅ |
| UDP | ❌ SSH 本身使用 TCP | ✅ |
| CTF 常見用途 | 登入遠端 Linux machine | 連接 challenge 的 IP + Port |

最簡單的記法：

```text
SSH = 我要「登入」那台 Server
nc  = 我要「連接」某個 IP:Port 並跟服務收發資料
```

例如：

```bash
ssh gabe@10.0.0.5
```

→ 我要登入 `10.0.0.5`。

```bash
nc 10.0.0.5 5000
```

→ 我要連接 `10.0.0.5` 上的 **port 5000**，跟那個 port 上的 service 溝通。

---

## 8. 今天順便學到的 Terminal 基礎

### 查看說明

很多 command 可以使用：

```bash
command --help
```

或：

```bash
command -h
```

但要注意：**不是每個 command 的 `-h` 都代表 help**，所以 `--help` 通常比較明確。

如果程式顯示：

```text
Pass me -h to learn what I can do
```

就是要你：

```bash
./program -h
```

把 `-h` 當作 command-line argument 傳給程式。

### ZIP 解壓縮

```bash
unzip filename.zip
```

### tar.gz 解壓縮

`.tar.gz` 可以理解成：

```text
tar 打包 + gzip 壓縮
```

解壓：

```bash
tar -xzf filename.tar.gz
```

其中：

```text
-x = extract
-z = gzip
-f = 指定 file
```

---

# 🧠 Day 1 Cheat Sheet

```bash
# 下載檔案
wget <URL>

# 查看檔案
ls

# 查看目前位置
pwd

# 加 executable 權限
chmod +x filename

# 執行目前 directory 的程式
./filename

# 查看程式說明
./filename -h

# 解壓 zip
unzip filename.zip

# 解壓 tar.gz
tar -xzf filename.tar.gz

# SSH 登入 Server
ssh username@server-ip

# Netcat 連接 IP:Port
nc server-ip port

# Netcat Listen
nc -l port
```

### Day 1 核心觀念

```text
wget     → Download
chmod +x → Make executable
./       → Execute
ssh      → Remote login
nc       → TCP/UDP connection & data transfer
Tab      → Autocomplete
ROT13    → Caesar-style substitution with shift 13
```