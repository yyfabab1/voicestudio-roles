# voicestudio-roles · 声音角色数据包（VoiceStudio 配套角色库）

> [VoiceStudio 声音角色工作台](https://github.com/yyfabab1/voicestudio-workbench) 的**角色数据包**：
> 27 个角色的切片素材、训练数据集与成品音频，带一份清洗过的 `roles.json` 索引。
>
> 与工作台**分仓**存放 —— 代码归代码，数据归数据：改代码不会动到你的素材库，
> 换素材库也不会把代码带着跑。

---

## 里面有什么

```
roles.json              # 角色索引（27 条：id / 名字 / 类型 / 训练状态 / 能力）
roles/<id>/             # 一个角色一个目录
  ├── role.json         #   角色元信息
  ├── slices/           #   切片素材（按静音切好的短音频）
  ├── rvc_dataset/      #   RVC 训练数据（F0 / HuBERT 特征等）
  ├── final/            #   成品（说话 / 唱歌的输出）
  ├── asr.list          #   识别出来的文本
  └── tone_index.json   #   语气索引
```

`roles.json` 可以直接覆盖工作台的 `data/roles.json`；`roles/` 整个目录放进 `data/` 下即可。

---

## 怎么用

```bash
# 1. 拿数据
git clone https://github.com/yyfabab1/voicestudio-roles.git

# 2. 拿工作台（它自己会带一份空的 data/）
git clone https://github.com/yyfabab1/voicestudio-workbench.git

# 3. 合起来：角色目录 + 索引放进工作台的 data/
cp -r voicestudio-roles/roles   voicestudio-workbench/data/
cp    voicestudio-roles/roles.json voicestudio-workbench/data/
```

然后按工作台 README 的「启动」跑起来就行 —— 启动脚本会自己拉起服务并打开
http://127.0.0.1:8756 。

---

## 角色清单（27 个）

覆盖小马宝莉、地狱客栈等作品的角色声模。完整清单（含 id、类型、训练状态）见
`roles.json`，或在工作台界面的角色墙上看卡片。

| 字段 | 说明 |
|---|---|
| `id` | 角色唯一标识，同时也是 `roles/` 下的目录名 |
| `name` | 中文名（市场装进来的角色会自动翻译成名） |
| `type` | 说话 / 唱歌 |
| 训练状态 | 有没有 RVC 歌声模型、已训到第几轮、能不能说话/唱歌 |

---

## 边界（如实说明）

| 项 | 情况 |
|---|---|
| **不含"大帝"角色** | 打包时显式排除，本仓只有另外 27 个角色 |
| **不含模型权重** | 说话权重在 GPT-SoVITS 整合包的 `GPT_weights_v5turbo/`，歌声模型在 RVC 的 `assets/weights/` —— 都在各自整合包里，不在本仓 |
| **不含原始视频** | 只留切好的音频切片与成品 |
| **声纹数据请注意** | 这些是声纹克隆素材。公开仓库意味着任何人都能拿到 —— 确认你有权公开这些声音再开放 |

---

## 相关

- 工作台代码：**[voicestudio-workbench](https://github.com/yyfabab1/voicestudio-workbench)**
- 打包工具：`tools/pack.py`（在工作台仓里，白名单式打包，排除 `data/` 与 `models/`）
