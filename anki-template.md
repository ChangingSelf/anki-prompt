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
