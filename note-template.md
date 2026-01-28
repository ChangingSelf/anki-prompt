# Anki 自定义卡片模板

## 笔记类型名称：SmartCard

### 字段（Fields）
1. **Front** - 问题
2. **Answer** - 核心答案
3. **Explain** - 解释说明（可选，支持多行）
4. **Mnemonic** - 助记（可选）

---

## 正面模板（Front Template）

```html
<div class="front">{{Front}}</div>
```

---

## 背面模板（Back Template）

```html
<div class="front">{{Front}}</div>

<hr id="answer">

<div class="back">
  <div class="answer">{{Answer}}</div>
  
  {{#Explain}}
  <div class="explain">{{Explain}}</div>
  {{/Explain}}
  
  {{#Mnemonic}}
  <div class="mnemonic">💡 {{Mnemonic}}</div>
  {{/Mnemonic}}
</div>
```

---

## 样式（Styling / CSS）

```css
/* ===== 整体卡片 ===== */
.card {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  font-size: 18px;
  line-height: 1.7;
  color: #333;
  background: #fafafa;
  padding: 24px;
  max-width: 600px;
  margin: 0 auto;
}

/* ===== 问题区 ===== */
.front {
  font-size: 20px;
  font-weight: 500;
  color: #222;
}

/* ===== 分隔线 ===== */
hr#answer {
  border: none;
  border-top: 2px solid #e0e0e0;
  margin: 20px 0;
}

/* ===== 背面容器 ===== */
.back {
  text-align: left;
}

/* ===== 核心答案区 ===== */
.answer {
  font-size: 20px;
  font-weight: 600;
  color: #1a73e8;
  background: #e8f0fe;
  padding: 14px 18px;
  border-radius: 8px;
  margin-bottom: 20px;
  border-left: 4px solid #1a73e8;
  line-height: 1.5;
}

/* ===== 解释说明区 ===== */
.explain {
  font-size: 16px;
  color: #444;
  background: #fff;
  padding: 16px 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  border: 1px solid #e0e0e0;
}

/* ===== 助记区 ===== */
.mnemonic {
  font-size: 15px;
  color: #5d4037;
  background: #fff8e1;
  padding: 12px 16px;
  border-radius: 8px;
  border-left: 4px solid #ffc107;
  line-height: 1.6;
}

/* ===== 基础HTML标签美化 ===== */

/* 加粗/关键词 */
b, strong {
  color: #c62828;
  font-weight: 600;
}

/* 段落小标题 */
h4 {
  font-size: 15px;
  font-weight: 600;
  color: #1565c0;
  margin: 16px 0 8px 0;
  padding-bottom: 4px;
  border-bottom: 1px solid #e3f2fd;
}
h4:first-child {
  margin-top: 0;
}

/* 列表 */
ul, ol {
  margin: 10px 0;
  padding-left: 24px;
}
li {
  margin: 8px 0;
  line-height: 1.6;
}

/* 代码 */
code {
  background: #f5f5f5;
  padding: 2px 8px;
  border-radius: 4px;
  font-family: "SF Mono", Monaco, Consolas, monospace;
  font-size: 0.9em;
  color: #d63384;
  border: 1px solid #e0e0e0;
}

/* 代码块 */
pre {
  background: #263238;
  color: #aed581;
  padding: 12px 16px;
  border-radius: 6px;
  overflow-x: auto;
  font-size: 14px;
  line-height: 1.5;
}
pre code {
  background: none;
  border: none;
  padding: 0;
  color: inherit;
}
```

---

## 导入方法

1. 打开 Anki → 工具 → 管理笔记类型
2. 点击「添加」→ 选择「添加: 基础」→ 命名为 `SmartCard`
3. 点击「字段」→ 添加字段：`Answer`, `Explain`, `Mnemonic`
4. 点击「卡片」→ 分别粘贴正面模板、背面模板、CSS样式
5. 保存

---

## 示例数据

**AI使用基础HTML标记结构，不写style，样式由上方CSS提供**

```json
{
  "deckName": "Java",
  "modelName": "SmartCard",
  "fields": {
    "Front": "什么是哈希碰撞？",
    "Answer": "不同对象通过哈希算法得到<b>相同hashCode值</b>",
    "Explain": "<h4>原因</h4><ul><li>哈希算法将<b>无限数据</b>映射到<b>有限范围</b></li><li>不同输入可能产生相同输出</li></ul><h4>影响</h4><ul><li>hashCode相等不能作为最终判断</li><li>需要用<code>equals()</code>进一步确认</li></ul>",
    "Mnemonic": "图书馆书架号相同，书的内容不一定相同"
  },
  "tags": ["hashCode", "哈希碰撞"]
}
```

**渲染效果（脱离模板也可读）：**

即使没有CSS，上面的HTML也能正常显示：
- `<b>` 加粗关键词
- `<h4>` 显示为小标题
- `<ul><li>` 显示为列表
- `<code>` 显示代码

---

# Cloze 填空卡片模板

## 笔记类型名称：Cloze（或自定义 SmartCloze）

### 字段（Fields）
1. **Text** - 包含填空标记的主内容
2. **Extra** - 补充说明（可选）

> 注：Anki内置的Cloze模板已有这两个字段，可直接修改样式；或创建新模板命名为 `SmartCloze`

---

## 正面模板（Front Template）

```html
<div class="cloze-card">
  <div class="cloze-text">{{cloze:Text}}</div>
</div>
```

---

## 背面模板（Back Template）

```html
<div class="cloze-card">
  <div class="cloze-text">{{cloze:Text}}</div>
  
  {{#Back Extra}}
  <hr id="extra">
  <div class="extra">{{Back Extra}}</div>
  {{/Back Extra}}
</div>
```

---

## 样式（Styling / CSS）

```css
/* ===== 整体卡片 ===== */
.card {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  font-size: 18px;
  line-height: 1.8;
  color: #333;
  background: #fafafa;
  padding: 24px;
  max-width: 600px;
  margin: 0 auto;
}

/* ===== Cloze卡片容器 ===== */
.cloze-card {
  text-align: left;
}

/* ===== 主文本区 ===== */
.cloze-text {
  font-size: 19px;
  color: #222;
  line-height: 1.9;
}

/* ===== 填空答案（正面显示[...]，背面显示答案） ===== */
.cloze {
  font-weight: 700;
  color: #1a73e8;
  background: #e8f0fe;
  padding: 2px 10px;
  border-radius: 4px;
  border-bottom: 2px solid #1a73e8;
}

/* ===== 未激活的填空（其他编号的cloze） ===== */
.cloze-inactive {
  color: #666;
  background: #f0f0f0;
  padding: 2px 8px;
  border-radius: 4px;
  text-decoration: underline;
  text-decoration-style: dotted;
  text-underline-offset: 3px;
}

/* ===== 分隔线 ===== */
hr#extra {
  border: none;
  border-top: 2px solid #e0e0e0;
  margin: 24px 0 20px 0;
}

/* ===== 补充说明区 ===== */
.extra {
  font-size: 16px;
  color: #444;
  background: #fff;
  padding: 16px 20px;
  border-radius: 8px;
  border: 1px solid #e0e0e0;
  border-left: 4px solid #4caf50;
}

/* ===== 基础HTML标签美化 ===== */

/* 加粗/关键词 */
b, strong {
  color: #c62828;
  font-weight: 600;
}

/* 段落小标题 */
h4 {
  font-size: 15px;
  font-weight: 600;
  color: #1565c0;
  margin: 16px 0 8px 0;
  padding-bottom: 4px;
  border-bottom: 1px solid #e3f2fd;
}
h4:first-child {
  margin-top: 0;
}

/* 列表 */
ul, ol {
  margin: 10px 0;
  padding-left: 24px;
}
li {
  margin: 8px 0;
  line-height: 1.6;
}

/* 代码 - 行内 */
code {
  background: #f5f5f5;
  padding: 2px 8px;
  border-radius: 4px;
  font-family: "SF Mono", Monaco, Consolas, monospace;
  font-size: 0.9em;
  color: #d63384;
  border: 1px solid #e0e0e0;
}

/* 代码块 */
pre {
  background: #263238;
  color: #aed581;
  padding: 12px 16px;
  border-radius: 6px;
  overflow-x: auto;
  font-size: 14px;
  line-height: 1.5;
}
pre code {
  background: none;
  border: none;
  padding: 0;
  color: inherit;
}

/* ===== 夜间模式适配 ===== */
.nightMode .card,
.night_mode .card {
  background: #1e1e1e;
  color: #e0e0e0;
}
.nightMode .cloze-text,
.night_mode .cloze-text {
  color: #e0e0e0;
}
.nightMode .cloze,
.night_mode .cloze {
  background: #1e3a5f;
  color: #64b5f6;
  border-bottom-color: #64b5f6;
}
.nightMode .cloze-inactive,
.night_mode .cloze-inactive {
  background: #2d2d2d;
  color: #999;
}
.nightMode .extra,
.night_mode .extra {
  background: #2d2d2d;
  border-color: #444;
}
.nightMode code,
.night_mode code {
  background: #2d2d2d;
  border-color: #444;
  color: #f48fb1;
}
```

---

## 导入方法

### 方法一：修改内置Cloze模板
1. 打开 Anki → 工具 → 管理笔记类型
2. 选择「Cloze」→ 点击「卡片」
3. 分别粘贴正面模板、背面模板、CSS样式
4. 保存

### 方法二：创建新模板（推荐）
1. 打开 Anki → 工具 → 管理笔记类型
2. 点击「添加」→ 选择「克隆: Cloze」→ 命名为 `SmartCloze`
3. 点击「卡片」→ 分别粘贴正面模板、背面模板、CSS样式
4. 保存

---

## 示例数据

**基础填空：**
```json
{
  "deckName": "Java",
  "modelName": "Cloze",
  "fields": {
    "Text": "HashMap的默认初始容量是 {{c1::16}}，默认负载因子是 {{c2::0.75}}",
    "Extra": ""
  },
  "tags": ["Java::集合", "HashMap"]
}
```

**带提示的填空：**
```json
{
  "deckName": "Java",
  "modelName": "Cloze",
  "fields": {
    "Text": "JVM堆内存分为 {{c1::新生代::Young}} 和 {{c2::老年代::Old}}",
    "Extra": "<ul><li>新生代：Eden + S0 + S1</li><li>老年代：存放长期存活对象</li></ul>"
  },
  "tags": ["JVM::内存"]
}
```

**带HTML美化：**
```json
{
  "deckName": "Java",
  "modelName": "Cloze",
  "fields": {
    "Text": "线程池核心参数：<br>• 核心线程数：<code>{{c1::corePoolSize}}</code><br>• 最大线程数：<code>{{c2::maximumPoolSize}}</code><br>• 空闲存活时间：<code>{{c3::keepAliveTime}}</code>",
    "Extra": "<h4>记忆技巧</h4>核心→最大→存活，从小到大的顺序"
  },
  "tags": ["Java::并发", "线程池"]
}
```

**对比记忆（同时填空）：**
```json
{
  "deckName": "Java",
  "modelName": "Cloze",
  "fields": {
    "Text": "<code>{{c1::==}}</code> 比较<b>地址</b>，<code>{{c1::equals()}}</code> 比较<b>内容</b>",
    "Extra": "基本类型用==，对象用equals()（需重写）"
  },
  "tags": ["Java::基础", "易混淆"]
}
```

---

## 样式特点说明

| 元素 | 样式效果 |
|------|----------|
| 当前填空 `.cloze` | 蓝色背景 + 蓝色下划线，醒目突出答案 |
| 未激活填空 `.cloze-inactive` | 灰色背景 + 虚线下划线，区分但不干扰 |
| 补充说明 `.extra` | 白底绿边框，与主内容区分 |
| 代码 `code` | 灰底粉色字，等宽字体 |
| 夜间模式 | 自动适配深色背景 |
