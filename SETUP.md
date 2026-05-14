# Setup local tools cho Resonance Tech

Hướng dẫn cài tools cần thiết để làm việc với org GitHub `nowa-technologies` từ máy local.

**Audience**: 👤 Members onboard (humans only — AI không cần).

**Time**: ~15 phút one-time setup.

---

## 1. Accept invitation + 2FA

1. Check email — accept invitation vào org `nowa-technologies`
2. Setup 2FA (Two-Factor Authentication) cho GitHub account:
   - GitHub Settings → Password and authentication → Two-factor authentication
   - **BẮT BUỘC** — không có 2FA sẽ bị kick khỏi org tự động
   - Recommend dùng app: Authy, Google Authenticator, hoặc 1Password
   - **Save recovery code** offline (in ra hoặc lưu password manager)

---

## 2. Cài tools

### macOS

```bash
# Git (thường đã có sẵn trên macOS)
git --version

# Nếu chưa có Git:
brew install git

# VS Code (editor recommended)
brew install --cask visual-studio-code

# GitHub CLI (optional, làm việc nhanh hơn qua command line)
brew install gh
```

### Windows

- Git: download từ https://git-scm.com/download/win
- VS Code: download từ https://code.visualstudio.com/
- GitHub CLI: download từ https://cli.github.com/

### Linux

```bash
# Debian/Ubuntu
sudo apt install git
sudo snap install code --classic
sudo apt install gh

# Arch
sudo pacman -S git code github-cli
```

---

## 3. Config Git local

```bash
git config --global user.name "Your Full Name"
git config --global user.email "yourname@resonancetech.co"
```

---

## 4. Authenticate `gh` CLI (optional but recommended)

```bash
gh auth login
```

Follow prompts:
1. **GitHub.com**
2. **SSH** (recommended)
3. **Generate new SSH key** (nếu chưa có) → press Enter for empty passphrase
4. **Title**: "GitHub CLI" (default)
5. **Login with web browser**
6. Copy 8-character code → press Enter → browser mở → paste code → Authorize

Verify:
```bash
gh auth status
```

Expected:
```
github.com
  ✓ Logged in to github.com account <username>
```

---

## 5. Test access

Clone workspace của bạn:
```bash
git clone git@github.com:nowa-technologies/<your-firstname>-workspace.git
cd <your-firstname>-workspace
```

Nếu thành công → setup OK ✓

---

## 6. Troubleshooting

### "Permission denied (publickey)" khi clone

→ SSH key chưa upload lên GitHub. Chạy:
```bash
gh auth refresh -s admin:public_key
```

### "git@github.com: Could not resolve hostname"

→ Kiểm tra internet. Nếu OK, thử HTTPS thay vì SSH:
```bash
git clone https://github.com/nowa-technologies/<your-firstname>-workspace.git
```

### "fatal: Authentication failed"

→ HTTPS yêu cầu personal access token thay vì password. Hoặc setup SSH (recommended).

### 2FA app bị mất

→ Liên hệ Andy/Grace ngay. Dùng recovery code đã save.

### Khác

→ Pings Andy/Grace qua Telegram.

---

## 7. Sau khi setup xong

→ Đọc [CONTRIBUTING.md](./CONTRIBUTING.md) — rules, conventions, workflow.
