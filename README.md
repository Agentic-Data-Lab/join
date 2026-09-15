# 申请加入 Agentic Data Lab 组织

本仓库是**加入组织（organization）的自助入口**：同学自己提交一个申请，管理员核对后一键放行，之后你会收到 GitHub 邀请邮件。

加入后可**只读**访问我们的文档仓库（`server_info`：服务器连接方式、硬件信息、账号权限等），
方便你，也方便**让你的 agent 自己去读**这些 Markdown 文档。

---

## 同学：三步加入

### 第 1 步：提交申请

点 [**New issue → 申请加入 Agentic Data Lab 组织**](https://github.com/Agentic-Data-Lab/join/issues/new/choose)，
填**中文姓名**（管理员按名字核对）和可选的补充说明，勾选两个确认项后提交。

### 第 2 步：等管理员核对

管理员看到申请后核对姓名，通过就点一下 `approved` 标签，之后**全自动**：工作流发出组织邀请、
在 issue 里回帖告知、打上 `invited` 标签并关闭 issue。

### 第 3 步：接受邀请

**邮件里点接受**（也可以在你的 [组织邀请页](https://github.com/orgs/Agentic-Data-Lab/invitation) 找到它）。

- 邀请**7 天过期**，过期了在 issue 里回帖让管理员重发；
- 接受后你会自动进入**只读团队**，无需再申请别的权限；
- 如果显示「已经是成员」，说明你之前就加入过，直接去读仓库即可。

---

## 规则

- **只读**：不要尝试修改组织内仓库的内容，需要改文档请告诉管理员；
- **不外传**：组织内**所有 private 仓库**的内容（含内网地址、共享盘口令等）一律不得对外传播，
  也不得转发给组外的人；
- 其他实验室资源从导航面板进入：<https://panel.jianke-yu.online/>；
- 详细条款见 [usage-policy.md](usage-policy.md)。

---

## 管理员：日常只需要点一下

同学的申请进来后，**你唯一要做的就是核对姓名 + 给 issue 加 `approved` 标签**，其余全自动：
解析只读团队 → 发出组织邀请（带上团队，接受即入组）→ 回帖告知 → 打 `invited` 标签 → 关闭 issue。
对方点邮件接受后，自动成为只读团队成员。

## 管理员：日常操作

| 想做什么 | 怎么做 |
| --- | --- |
| **批准** | 核对姓名/中文名/导师与实验室名单是否对得上，然后给 issue 加 **`approved`** 标签 → 工作流自动发邀请、回帖、打 `invited` 标签并关闭 issue |
| **驳回** | 加 **`rejected`** 标签 + 回帖说明原因 + 关闭 issue |
| **重发邀请** | 把 `invited` 标签去掉再加回 `approved`（或直接到组织 People 页面重发）；邀请 7 天过期 |
| **撤销资格** | 组织 → People → 找到该成员 → Remove from organization（或 `DELETE /orgs/{org}/memberships/{username}`） |
| **看谁还没接受** | 组织 → People → **Pending invitations**（可批量取消/重发） |
| **核对身份** | 组织成员列表按 Name（拼音）排序即可对号入座；`server_info/docs/user_info.md` 里有实验室账号对照表 |

### 需要配置的东西（一次性）

1. **Secret `ORG_ADMIN_TOKEN`**（Settings → Secrets and variables → Actions → New repository secret）
   - 细粒度 PAT：Organization permissions → **Members: Read and write**，Repository access 选本仓库；
   - 或经典 PAT：勾 `admin:org`。
   - 到期或轮换时更新这个 secret 即可，工作流不用改。
2. **变量（可选，通常不用设）** Settings → Secrets and variables → Actions → **Variables**
   - `ORG_NAME`（默认 `Agentic-Data-Lab`）
   - `TEAM_SLUG`（默认 `basic-team`）、`TEAM_NAME`（默认 `Basic Team`）
   - 团队是**按 slug 或显示名自动解析**的（忽略大小写、空格、连字符），所以团队改名、或只记得显示名
     （`Basic Team`）都不会解析错；万一两个候选都不对，工作流会打印出组织下的团队清单让你照抄。

### 标签含义

| 标签 | 含义 |
| --- | --- |
| `join-request` | 新申请，待管理员核对（表单自动打） |
| `approved` | 管理员已批准 → 触发邀请工作流 |
| `invited` | 已发出邀请（工作流自动打） |
| `rejected` | 未通过 |

---

## 安全设计（为什么外人也开不了口子）

- 本仓库是**公开**的（否则没加入组织的人无法提交 issue），但**任何人提交 issue 都不会自动被拉进组织**：
  工作流只在 issue 被加上 **`approved`** 标签时才触发，而打标签需要仓库写权限 = 管理员；
- 工作流**不 checkout 代码、不执行 issue 里的任何内容**，只按 issue 作者的身份调 GitHub API 发邀请；
- 组织级操作只用一个权限最小的 PAT（`ORG_ADMIN_TOKEN`），仓库级操作（回帖/标签/关闭）用默认 `GITHUB_TOKEN`；
- 邀请不是成员资格：对方必须自己点接受才生效，管理员随时可在 People 页面撤销。

## 常见问题

**Q：我改了 Name，但还是显示旧名字？**
A：组织成员列表会有几分钟缓存；确认改的是 Public profile 的 Name，而不是 Bio 或公司字段。

**Q：我的 GitHub 名字已经注册成别的了，能改吗？**
A：能。login（登录名）可以改一次（设置里 Change username），但**没必要**——只改 Name 就够了。

**Q：邀请邮件没收到？**
A：检查垃圾箱；也可以在 [组织邀请页](https://github.com/orgs/Agentic-Data-Lab/invitation) 找到。7 天过期就在申请 issue 里回帖。

**Q：我只是想让 agent 读文档，一定要加入组织吗？**
A：目前是这样（文档仓库是私有的）。另外站点上有只读的 Markdown 端点和 `llms.txt`，只要管理员给你口令，不加入组织也能读——需要的话找管理员。
