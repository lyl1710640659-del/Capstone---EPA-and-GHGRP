# 第一次用 GitHub：从这里开始

你的仓库：<https://github.com/lyl1710640659-del/Capstone---EPA-and-GHGRP>

全程约 10 分钟。**照着抄就行，不需要懂 git。**

> 做完记得把这个文件删掉——它是给你看的说明，不该出现在公开仓库里。

---

## 第 1 步 · 打开终端

Dock 里那个黑色的 `>_` 图标（Terminal）。
或者按 `Command + 空格`，输入 `terminal`，回车。

打开后会看到一个可以打字的窗口。**下面每一段代码，复制粘贴进去，按回车。**

---

## 第 2 步 · 进入文件夹并清理

一次性粘贴这四行（可以一起粘，会依次执行）：

```bash
cd "/Users/longyiling/Desktop/26 Fall PhD/Capstone/repo"
rm -rf .git
rm -f output/fig1_tier3_diagnostics.png
rm -f .DS_Store
```

在做什么：

- 第 1 行：进入 repo 文件夹
- 第 2 行：删掉我之前建的那个坏掉的 git 记录（在你的电脑上权限正常，删得掉）
- 第 3 行：删掉郅老师 RA 数据的诊断图——**这个不能公开**
- 第 4 行：删掉 macOS 的隐藏垃圾文件

没有任何输出 = 成功。git 相关的东西是"没消息就是好消息"。

---

## 第 3 步 · 告诉 git 你是谁

只需要做这一次，以后所有仓库都不用再设：

```bash
git config --global user.name "Yiling Long"
git config --global user.email "lyl1710640659@gmail.com"
```

---

## 第 4 步 · 建立仓库并提交

```bash
git init
git add -A
git commit -m "GHGRP reporting thresholds: descriptive analysis and off-ramp test"
git branch -M main
git remote add origin https://github.com/lyl1710640659-del/Capstone---EPA-and-GHGRP.git
```

`git commit` 那行会打印一串文件名，正常。

---

## 第 5 步 · 推送（认证在这一步）

```bash
git push -u origin main
```

**GitHub 已经不接受账号密码了**，所以这里会有一个坎。两条路，选一条：

### 路线 A · GitHub Desktop（**推荐，第一次用就选这个**）

1. 下载 <https://desktop.github.com/> ，安装，打开
2. 用你的 GitHub 账号登录（会跳转浏览器，点同意）
3. 菜单栏 **File → Add Local Repository**
4. 选 `/Users/longyiling/Desktop/26 Fall PhD/Capstone/repo`
5. 右上角点 **Publish repository** 或 **Push origin**

装完之后，终端里的 `git push` 也能直接用了（它帮你存好了凭证）。
以后每次改完东西，在 GitHub Desktop 里点两下就能更新，不用记命令。

### 路线 B · 用 Token 当密码

1. 去 <https://github.com/settings/tokens> → **Generate new token (classic)**
2. Note 随便填（比如 `capstone`），Expiration 选 90 days
3. 勾选 **repo**（第一个大类，勾它就会自动勾上下面几个）
4. 拉到底 → **Generate token** → **立刻复制那串字符**（离开页面就再也看不到了）
5. 回终端再跑一次 `git push -u origin main`
   - `Username:` 输入 `lyl1710640659-del`
   - `Password:` **粘贴那串 token**（终端里粘贴时不会显示任何字符，这是正常的，粘完直接回车）

---

## 第 6 步 · 打开 GitHub Pages（**不做这步，HTML 就是废的**）

> GitHub 不会渲染独立的 `.html` 文件——直接点开只能看到源代码。
> 必须开 Pages，这就是我把 HTML 放在 `docs/` 里的原因。

1. 打开你的仓库页面
2. 上方 **Settings**
3. 左侧栏往下找 **Pages**
4. **Source** 选 `Deploy from a branch`
5. **Branch** 选 `main`，右边的文件夹下拉选 **`/docs`**
6. 点 **Save**

等 1–2 分钟（可以去 Actions 标签页看进度），然后打开：

```
https://lyl1710640659-del.github.io/Capstone---EPA-and-GHGRP/
```

README 里的链接已经按这个地址写好了。

---

## 第 7 步 · 检查

打开 <https://github.com/lyl1710640659-del/Capstone---EPA-and-GHGRP> 确认：

- [ ] 首页显示 README（标题是 *Disclosure thresholds and the exit margin*）
- [ ] 点 `01_descriptive_sweep.ipynb` → 能看到文字、代码**和图**
- [ ] 有 `docs/`、`output/`、`ghgrp_load.py`
- [ ] **没有** `data/` 文件夹（31MB 的 EPA 数据不该上传）
- [ ] **没有** `fig1_tier3_diagnostics.png`
- [ ] **没有** `PUSH_TO_GITHUB.md`（如果还在，删掉再推一次）
- [ ] Pages 链接能打开看板

---

## 第 8 步 · 发给 John

只发主仓库地址就够了，README 里有两个入口：

```
https://github.com/lyl1710640659-del/Capstone---EPA-and-GHGRP
```

邮件草稿：

> Hi John,
>
> Ahead of our meeting I put the descriptive work up here:
> https://github.com/lyl1710640659-del/Capstone---EPA-and-GHGRP
>
> The short version: the bunching design I came in with doesn't survive — the sample is
> truncated at the reporting threshold, and the density is smooth at 15,000 either way. But
> the cessation provision in 40 CFR 98.2(i) turns out to bite hard. Facilities eligible to
> stop reporting leave at 21% a year against 1.5% for those that aren't, and the years they
> spend below each threshold before leaving pile up at exactly the statutory waiting periods,
> with placebo thresholds null.
>
> There's one large confound I found and handled (the 2014–16 oil collapse), and one gap I
> can't close with this data — I can see facilities stop *reporting*, not whether they stop
> *operating*. Happy to walk through both tomorrow.
>
> Yiling

---

## 以后怎么更新

改完东西之后：

**GitHub Desktop**：打开 → 左边会列出改了哪些文件 → 左下角写一句说明 →
**Commit to main** → 右上 **Push origin**。

**终端**：

```bash
cd "/Users/longyiling/Desktop/26 Fall PhD/Capstone/repo"
git add -A
git commit -m "写一句改了什么"
git push
```

Pages 会在一两分钟后自动更新。

> **注意**：`repo/` 是 `analysis/` 的一份拷贝。平时改代码改 `analysis/` 里的，
> 然后把 `01_descriptive_sweep.ipynb`、`ghgrp_load.py`、`output/f*.png`、
> 以及 `Meetings/0728/GHGRP_findings_0728.html`（要改名成 `repo/docs/index.html`）拷过去。
> 嫌麻烦的话之后可以直接把 `analysis/` 变成 repo——`data/` 已经在 `.gitignore` 里了。

---

## 出错了怎么办

| 报错 | 意思 | 怎么办 |
|---|---|---|
| `remote origin already exists` | 第 4 步跑了两次 | `git remote remove origin` 再重跑那一行 |
| `Authentication failed` | 认证没过 | 回第 5 步，用路线 A |
| `Support for password authentication was removed` | 你输了账号密码 | 密码位置要填 token，不是密码 |
| `src refspec main does not match any` | 还没 commit | 回第 4 步把 `git add` 和 `git commit` 跑完 |
| `nothing to commit` | 没有改动 | 正常，不用管 |
| Pages 链接 404 | 还在部署 / 路径没选对 | 等 2 分钟；确认 Branch 是 `main` + `/docs` |

看到 `warning:` 开头的可以忽略，`error:` 和 `fatal:` 才是真问题。
