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
├── nowa-os-knowledge-hub             ← NOWA product knowledge hub (mọi người read)
├── nowa-mkt-pre-launch-ads-2026       ← Marketing campaign 2026 (marketing own)
├── personal-workspace-<firstname>     ← Personal workspace của bạn (private)
└── ... (repos khác mỗi team tự tạo theo nhu cầu)
```

**Quy tắc về scope repo**:
- Personal workspace: **chỉ docs/notes**, không chứa project có deliverable
- Bất kỳ project (cá nhân hay team): repo riêng theo naming convention
- Khi nghi ngờ: separate repo (tránh nest project trong personal workspace)

**Future repos** mỗi team có thể tạo theo nhu cầu:
- `nowa-mkt-ads-tracking-2026` (marketing automation)
- `nowa-des-brand-guideline` (design, evergreen)
- `nowa-ba-product-specs` (BA)
- `andy-dev-side-tool` (Andy's personal dev project)
- ... theo naming convention: xem §4

### 1.2 Teams

| Team | Members | Quyền |
|---|---|---|
| `@owners` | Andy, Grace | Full admin |
| `@marketing` | Marketing team | Owner marketing repos |
| `@design` | Design team | Owner design repos |
| `@business-analyst` | BA team | Owner BA repos |
| `@engineering` | Dev team | Owner eng repos |
| `@human-resources` | HR team | Owner HR repos |
| `@customer-support` | CS team | Owner CS workstream/repos |
| `@product-manager` | PM team | Own product/pawcast PM repos |
| `@research-and-development` | R&D team | Own R&D repos |
| `@all-staff` | Toàn company | Read shared repos |

### 1.3 Personal workspace

Mỗi member có 1 workspace riêng: `nowa-technologies/personal-workspace-<firstname>`.

- Private — chỉ bạn + `@owners` thấy
- Bạn là Admin — full control

**Dùng cho**:
- 📝 Draft documents trước khi share team
- 💭 Notes, research, AI conversations
- 📚 Lưu trữ tài liệu cá nhân liên quan org
- ☁️ Backup local work lên cloud
- 🤖 Working memory cho AI agents của bạn

**KHÔNG dùng cho**:
- ❌ Private/personal projects (code, app dev, experiments có deliverable) → tạo repo riêng theo naming convention `{firstname}-{team-or-aspect}-{project}`
  - Vd: `andy-dev-side-tool`, `grace-pm-tool`
- ❌ Code projects → repo riêng
- ❌ Bất kỳ deliverable có scope project riêng → repo độc lập

→ **Lý do**: AI agents đọc workspace như **personal context store** (docs/notes), không expect parse code structure phức tạp. Mix project vào sẽ làm agent confuse về scope.

---

## 2. Permission model — BDFL

Mỗi repo có **1 task owner** = người duy nhất merge được vào `main`.

| Loại repo | Task owner |
|---|---|
| Personal workspace `personal-workspace-<firstname>` | Bạn |
| Personal projects `<firstname>-<team>-<project>` | Bạn |
| Team repos (vd `nowa-mkt-pre-launch-ads-2026`) | Team lead / PIC project |
| Shared repos (`knowledge-hub`, `agent-skills`) | `@owners` (Andy, Grace) |

**Workflow ý nghĩa**:
- Bạn có thể tạo PR vào bất kỳ repo nào bạn có access
- Nhưng chỉ task owner mới merge được
- Trên personal workspace + personal projects, bạn là task owner → tự merge được mọi PR của mình

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

## 4. Naming conventions

### 4.1 Repo name

**Pattern**: `{scope}-{team-or-aspect}-{project}[-{time}]`

| Level | Options | Required |
|---|---|---|
| Scope (level 1) | `rt-` (RT-wide), `nowa-`, `teampal-`, `cross-`, **`{firstname}-`** (personal project) | ✓ |
| Team abbrev (level 2) | `mkt`, `des`, `ba`, `dev`, `hr` | ✓ (hoặc aspect) |
| Aspect (level 2 nếu không team) | `org`, `os`, `fin`, `legal`, `tools` | ✓ (hoặc team) |
| Project (level 3) | kebab-case mô tả | ✓ |
| Time (level 4) | `2026`, `2026-q2`, `may2026` | Optional (khi time-bounded) |

**Examples**:

| Repo | Phân tích |
|---|---|
| `nowa-mkt-pre-launch-ads-2026` | NOWA × marketing × pre-launch-ads × 2026 |
| `rt-agent-skills` | RT-wide × skills (scope skip cho cực kỳ general repos) |
| `nowa-os-knowledge-hub` | NOWA × org-level × knowledge-hub |
| `nowa-des-brand-guideline` | NOWA × design × brand-guideline (evergreen) |
| `nowa-os-customer-support` | NOWA × operating system aspect × customer-support |
| `andy-dev-side-tool` | Andy personal × dev × side-tool |
| `grace-pm-tool` | Grace personal × project management × tool |
| `cross-mkt-channel-strategy` | Cross-product × marketing × channel-strategy |

### 4.2 Branch name

**Pattern**: `{team-abbrev}/{your-firstname}/{short-description}`

**Optional với type**: `{team-abbrev}/{your-firstname}/{type}/{short-description}`

**Type vocabulary**: `feature`, `fix`, `content`, `docs`, `refactor`, `experiment`

**Rules**:
- ✅ kebab-case (lowercase, hyphens)
- ✅ Max 5 từ trong `short-description`
- ✅ Author = firstname (khớp với personal workspace name)
- ❌ Không underscore, không camelCase, không spaces
- ❌ Không tên ambiguous: `update`, `fix`, `change` (phải có context)

**Examples**:
```
mkt/amy/audience-fintech-lp                      ← Default form
mkt/amy/feature/audience-fintech-lp              ← With type
mkt/amy/content/fintech-headline-update          ← Content change
mkt/amy/fix/mobile-overflow-on-fintech-lp        ← Bug fix
mkt/amy/experiment/variant-b-pricing-section     ← A/B test
des/grace/refactor/component-library-tokens      ← Design refactor
dev/huyle/fix/auth-flow-edge-case                ← Dev fix
```

### 4.3 File & folder

| Item | Convention | Example |
|---|---|---|
| Folder | `lowercase`, kebab-case | `landing-pages/`, `design-assets/` |
| File `.md` | `kebab-case.md` | `current-plan.md`, `brand-guideline.md` |
| Special files | `README.md`, `LICENSE` (uppercase convention) | |
| Code files | Follow language convention | `.ts` kebab/camel, `.py` snake_case |

### 4.4 Commit message

**Format**: `{Verb in imperative} {what changed}`

✅ **Good**:
```
Add Q3 launching plan for fintech audience
Fix typo in brand guideline
Update README with new naming convention
Refactor component library structure
```

❌ **Bad**:
```
updated stuff
fix
WIP
changes from yesterday
my work
```

**Rules**: Imperative tense ("Add", không "Added"), first letter capital, max ~50 ký tự, no period at end.

### 4.5 PR title

**Format**: `{Team}: {Action} {what}`

✅ **Good**:
```
Marketing: Add fintech audience LP variant
Design: Refactor brand color tokens
BA: Update API spec for v2 endpoints
```

❌ **Bad**:
```
update
my PR
new stuff
amy's work
```

### 4.6 Khi nào tạo repo mới vs folder trong repo có sẵn?

**Default: folder, không tạo repo mới.** Repo proliferation khó manage.

**Decision table — 10 situations**:

| Tình huống | Decision |
|---|---|
| Sub-section của project hiện tại, cùng team, cùng release cycle | **Folder** |
| Sub-project rõ ràng, cùng team, cùng release | **Folder** với name rõ ràng |
| Project mới, team khác own | **Repo mới** |
| Campaign năm sau (vd `nowa-mkt-launch-2027`) | **Repo mới** (time-bounded) |
| Variant của LP hiện tại | **Folder** trong `{repo}/variants/` |
| Asset chung được dùng bởi nhiều projects | **Repo riêng** (vd `nowa-des-brand-guideline`) |
| Skill mới cho AI agents | **Folder** trong `rt-agent-skills/skill-name/` |
| Document evergreen về product | **Folder** trong `nowa-os-knowledge-hub/` |
| Internal tool standalone | **Repo mới** (vd `rt-tools-deploy-helper`) |
| Personal/side project có deliverable | **Repo riêng** `{firstname}-{team}-{project}` |

**Re-evaluate khi nào split folder thành repo riêng**:
- Folder grow >500 files hoặc >500MB
- Có team khác muốn own folder đó
- Cần CI/CD riêng cho folder
- Cần public folder đó

### 4.7 Sub-project structure (folders inside repo)

**Khi 1 repo chứa nhiều sub-projects/variants**, organize theo folder:

```
nowa-mkt-pre-launch-ads-2026/
├── README.md                  ← Navigation
├── shared/                    ← Components, styles, assets dùng chung
│   ├── components/
│   ├── styles/
│   └── assets/                ← Logo, icons (ảnh nhỏ optimized)
├── audiences/                 ← Mỗi audience 1 folder
│   ├── fintech/
│   │   ├── index.html
│   │   ├── content.md         ← Copy/text
│   │   ├── layout.css         ← Layout-specific
│   │   └── logic.js           ← Form behavior, tracking
│   ├── ecommerce/
│   └── saas/
├── experiments/               ← A/B variants
│   └── variant-b-pricing/
└── deploy.config.json
```

→ Folder organize theo **dimension chính** (audience, type, time) + **type of change** (content/layout/logic).

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

Required cho mọi repo.

### 6.2 README per folder (knowledge-hub, agent-skills)

Trong các repo content-heavy (`nowa-os-knowledge-hub`, `rt-agent-skills`,...), **mỗi folder có 1 `README.md`** để navigate. Mục đích: cả human + AI hiểu folder này là gì khi mở.

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

### 7.4 Để AI agents tự follow naming convention

Để Claude / AI agents của mọi người **tự follow** convention §4 khi tạo repo, mỗi member thêm block dưới vào `~/.claude/CLAUDE.md` (rule global, áp mọi project) — hoặc per-project `/CLAUDE.md`:

```
## GitHub repo creation in nowa-technologies org
Always follow naming convention from:
https://github.com/nowa-technologies/.github/blob/main/CONTRIBUTING.md §4
Pattern: {scope}-{team-or-aspect}-{project}[-{time}]
- scope: rt- (RT-wide), nowa-, teampal-, cross-, or {firstname}- (personal)
- team: mkt, des, ba, dev, hr
- aspect (when no team): org, os, fin, legal, tools
- project: kebab-case
- time (optional): 2026, 2026-q2, may2026
Special:
- personal-workspace-{firstname} (workspace pattern, không follow main rule)
- Personal workspace: chỉ docs/notes, không project có deliverable
- Personal projects: separate repo theo pattern
Before creating any repo:
1. Validate name matches pattern
2. If unsure, ask user before creating
3. Reference CONTRIBUTING.md for examples
```

→ Lý do: AI agent local không tự đọc repo org mỗi lần; có rule trong `CLAUDE.md` thì agent luôn có context → không tạo repo sai tên.

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
Last updated: 2026-06-29
