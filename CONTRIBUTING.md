# Contributing to Resonance Tech

Source of truth cho convention, workflow, rules trên GitHub Org `nowa-technologies`.

**Audience**: 
- 👤 **Members** đọc khi onboard + reference khi làm việc
- 🤖 **AI agents** đọc làm context khi gen code/content cho org

**Khi nghi ngờ về convention/workflow → ref file này.**

Setup local tools (cài git, gh CLI...) ở doc riêng: [SETUP.md](./SETUP.md)

---

## 1. Org structure

### 1.1 Repos trong org

```
nowa-technologies/
├── .github                            ← Org profile + CONTRIBUTING (this file)
├── rt-agent-skills                    ← AI skills là company asset (mọi người read)
├── rt-organizational-foundation       ← Org info, structure, mission (mọi người read)
├── nowa-org-knowledge-hub             ← NOWA product knowledge hub (mọi người read)
├── nowa-mkt-pre-launch-ads-2026       ← Marketing campaign 2026 (marketing own)
├── <firstname>-workspace              ← Personal workspace của bạn (private)
└── ... (repos khác mỗi team tự tạo theo nhu cầu)
```

**Future repos** mỗi team có thể tạo theo nhu cầu:
- `nowa-mkt-ads-tracking-2026` (marketing automation)
- `nowa-des-brand-guideline` (design, evergreen)
- `nowa-ba-product-specs` (BA)
- ... theo naming convention: `{scope}-{team}-{project}[-{time}]`

### 1.2 Teams

| Team | Members | Quyền |
|---|---|---|
| `@owners` | Andy, Grace | Full admin |
| `@marketing` | Marketing team | Owner marketing repos |
| `@design` | Design team | Owner design repos |
| `@business-analyst` | BA team | Owner BA repos |
| `@engineering` | Dev team | Owner eng repos |
| `@hr` | HR team | Owner HR repos |
| `@all-staff` | Toàn company | Read shared repos |

### 1.3 Personal workspace

Mỗi member có 1 workspace riêng: `nowa-technologies/<firstname>-workspace`.

- Private — chỉ bạn + `@owners` thấy
- Bạn là Admin — full control
- Dùng làm: draft, notes, AI conversations, side projects, backup local work

---

## 2. Permission model — BDFL

Mỗi repo có **1 task owner** = người duy nhất merge được vào `main`.

| Loại repo | Task owner |
|---|---|
| Personal workspace `<firstname>-workspace` | Bạn |
| Team repos (vd `nowa-mkt-pre-launch-ads-2026`) | Team lead / PIC project |
| Shared repos (`knowledge-hub`, `agent-skills`) | `@owners` (Andy, Grace) |

**Workflow ý nghĩa**:
- Bạn có thể tạo PR vào bất kỳ repo nào bạn có access
- Nhưng chỉ task owner mới merge được
- Trên personal workspace, bạn là task owner → tự merge được mọi PR của mình

---

## 3. Daily workflow

### 3.1 Standard PR flow

```bash
# 1. Update local main
git checkout main
git pull

# 2. Tạo branch mới
git checkout -b <team-abbrev>/<your-firstname>/<short-description>
# Ví dụ: git checkout -b mkt/amy/audience-fintech-lp

# 3. Làm việc, commit thường xuyên
git add <files>
git commit -m "<short imperative description>"

# 4. Push branch lên remote
git push -u origin <team-abbrev>/<your-firstname>/<short-description>

# 5. Tạo Pull Request trên GitHub web
# → Repo URL → "Compare & pull request" button

# 6. Đợi task owner review + merge
# (Hoặc tự merge nếu là task owner / personal workspace)

# 7. Sau khi PR merged, update local
git checkout main
git pull
git branch -d <team-abbrev>/<your-firstname>/<short-description>
```

### 3.2 Trong personal workspace

Workspace cá nhân: free style hơn. Bạn có thể:
- Push thẳng vào main (vì là task owner)
- Hoặc tạo branch + PR + self-merge nếu muốn track history rõ
- Commit không cần message quá formal — đây là không gian cá nhân

### 3.3 Quick edit qua GitHub web

Cho thay đổi nhỏ (typo, edit 1 dòng):
1. Vào repo trên GitHub web
2. Click vào file → pencil icon (Edit)
3. Sửa, scroll xuống "Commit changes"
4. Chọn "Create a new branch and start a pull request"
5. Tạo PR

---

## 4. Naming conventions (quick reference)

**Source of truth**: [naming-conventions.md](../../structure/naming-conventions.md) — đọc khi cần deep-dive.

### Repo name

Pattern: `{scope}-{team-or-aspect}-{project}[-{time}]`

| Level | Options |
|---|---|
| Scope (level 1) | `rt-` (company-wide), `nowa-`, `teampal-`, `cross-` |
| Team abbrev (level 2) | `mkt`, `des`, `ba`, `dev`, `hr` |
| Aspect (level 2 nếu không team) | `org`, `ops`, `fin`, `legal`, `tools` |
| Project (level 3) | kebab-case mô tả |
| Time (level 4 optional) | `2026`, `2026-q2`, `may2026` |

**Examples**:
- `nowa-mkt-pre-launch-2026` (NOWA × marketing × pre-launch × 2026)
- `rt-agent-skills` (RT-wide, không team)
- `nowa-org-knowledge-hub` (NOWA × org-level × knowledge-hub)
- `nowa-des-brand-guideline` (NOWA × design × brand-guideline, evergreen)

### Branch name

Pattern: `{team-abbrev}/{your-firstname}/{short-description}`

Optional với type: `{team-abbrev}/{your-firstname}/{type}/{short-description}`
- Type vocabulary: `feature`, `fix`, `content`, `docs`, `refactor`, `experiment`

**Examples**:
- `mkt/amy/audience-fintech-lp`
- `des/grace/feature/logo-refresh`
- `dev/john/fix/login-flow`

### Other

| Item | Convention | Example |
|---|---|---|
| Folder | `lowercase`, kebab-case | `landing-pages/` |
| File `.md` | `kebab-case.md` | `current-plan.md` |
| Special files | `README.md` (per folder = navigation), `LICENSE` | |
| Commit message | Imperative, capital first, no period | "Add Q2 launching plan" |
| PR title | `{Team}: {Action} {what}` | "Marketing: Add fintech LP variant" |

### Khi nào tạo repo mới vs folder?

**Default: folder, không tạo repo mới.** Tạo repo mới chỉ khi:
- Team khác own
- Release/deploy cycle khác
- Access permission khác (vd confidential)
- Sẽ public/share external
- >2GB hoặc >500 files

Xem decision tree đầy đủ trong [naming-conventions.md §2](../../structure/naming-conventions.md).

---

## 5. File rules

### ✅ Cho phép trong git

- Text: `.md`, `.txt`, `.csv`, `.json`, `.yaml`
- Code: `.html`, `.css`, `.js`, `.py`, `.tsx`, etc.
- Ảnh optimized cho web: `.jpg`, `.png`, `.svg`, `.webp` (<10MB mỗi file)
- Config: `.env.example` (template), `.gitignore`

### ❌ KHÔNG commit vào git

- **Secrets**: `.env`, credentials, API keys, certificates → ngay cả accidentally cũng đừng
- **File binary lớn**: video, audio, file >10MB → để Google Drive
- **Raw design files**: `.psd`, `.ai`, `.sketch` → Drive
- **OS junk**: `.DS_Store`, `Thumbs.db` (đã có trong `.gitignore` template)

Nếu lỡ commit secret → báo `@owners` ngay, rotate credentials.

---

## 6. Convention cho `README.md`

`README.md` đóng 2 vai trò tùy vị trí:

### 6.1 README ở **root** repo

Giới thiệu tổng quan repo: purpose, status, owner, structure, how to use.

Required cho mọi repo. Template trong `nowa-technologies/.github/templates/`.

### 6.2 README per folder (knowledge-hub, agent-skills)

Trong các repo content-heavy (`nowa-org-knowledge-hub`, `rt-agent-skills`,...), **mỗi folder có 1 `README.md`** để navigate. Mục đích: cả human + AI hiểu folder này là gì khi mở.

Pattern:
```markdown
# {Folder name}

## What's here
<Mô tả 1-2 câu folder này chứa gì>

## When to update
<Khi nào content cần update — vd: "Sau mỗi quarter", "Khi có decision mới">

## Owner
<Team hoặc người chịu trách nhiệm content>

## Related
- Link sang folder/repo liên quan
```

→ Khi AI agent đọc folder, tự động lấy README.md làm context. Không cần file metadata riêng.

---

## 7. AI workflow

### 7.1 Tag `@claude` trong PR (sắp enable)

Sau khi org cài Claude GitHub App:
- Comment vào PR: `@claude review this change`
- Claude tự động review code/content, comment inline

### 7.2 Claude.ai connect repo qua MCP

Members có thể connect Claude.ai chat trực tiếp tới repo:
- Settings trong Claude.ai → MCP connectors → GitHub
- Authenticate với org `nowa-technologies`
- Chat với Claude: "đọc launching plan trong knowledge-hub" → Claude tự đọc

### 7.3 Local Claude Code

Workflow cũ vẫn work bình thường:
- Clone repo về local
- Mở Claude Code
- Làm việc, commit, push

---

## 8. Khi nào hỏi help

| Situation | Channel |
|---|---|
| Git command lỗi, không biết fix | Telegram |
| Workflow không rõ | Telegram, hoặc hỏi Andy/Grace |
| Cần access vào repo mới | Pings Grace |
| Forgot 2FA → bị lock out | Email Andy |
| Lỡ commit secret | **NGAY LẬP TỨC** pings Andy + Grace |
| Suggest convention/process | Tạo PR vào file này (`CONTRIBUTING.md`) |

---

## 9. Update file này

Convention này là **living document**. Nếu thấy chỗ nào cần improve:
1. Tạo PR sửa file `CONTRIBUTING.md`
2. `@owners` review + merge
3. Announce trong Telegram

---

Owner: `@nowa-technologies/owners`
Last updated: 2026-05-12
