# 追光时间轴

这是一个静态时间轴网站，用来整理王允宸相关活动、作品、演出、杂志、商务与里程碑资料。



## 檔案結構

```text
index.html      # 时间轴网站主体
data.json       # 主要事件资料来源
```

## 主要功能

- 新到旧排序：预设载入近期年份，较旧年份自动合并成区间。
- 多语言：支援简中、繁中、英文切换。
- 类别筛选：可依活动类别过滤时间轴。
- 搜寻：支援简中、繁中、英文名称与描述搜寻，也可搜寻日期、时间、类别。
- 历史上的今天：根据使用者本地日期显示过去年份同月同日活动。
- 那年此日：事件卡片内会显示同月同日、不同年份的相关活动。
- 事件卡片：滑鼠靠近或触控开启后显示日期、类别、描述与连结。

## 目前分類

目前 `data.json` 使用以下分類：

```text
里程碑、商务、商演、Live、音乐剧、访谈/电台、典礼、时尚、综艺、见面会、作品、杂志、其他演出、其他
```

分類順序、URL slug、多語言名稱與顏色定義在 `index.html` 中：

```js
CATEGORY_ORDER
CATEGORY_SLUG
I18N.*.catLabel
CAT_CLASS
```

## data.json 格式

每笔事件是一个物件，建议包含以下栏位：

```json
{
  "date": "2026-06-28",
  "time": "13:00",
  "category": "见面会",
  "name-zh": "2026生日主题签售会",
  "name-tw": "2026生日主題簽售會",
  "name-en": "2026 Birthday Signing Event",
  "desc-zh": "補充說明",
  "desc-tw": "補充說明",
  "desc-en": "Additional notes",
  "link": "https://example.com"
}
```

### 栏位说明

- `date`: 必填，格式建议为 `YYYY-MM-DD`。
- `time`: 选填，格式建议为 `HH:MM`。
- `category`: 必填，需对应既有分类。
- `name-zh`, `name-tw`, `name-en`: 活动名称。若某语言缺漏，页面会依设定回退显示其他语言。
- `desc-zh`, `desc-tw`, `desc-en`: 补充描述。可留空。
- `link`: 原始来源或相关连结。可留空。

## 新增资料注意事项

可通过PR提交或留下ISSUE等站子后续处理

1. 新增事件时，请尽量补齐简中、繁中、英文名称。
2. 若只知道一种语言，也可以先填一种，页面会回退显示。
3. 同一天多个活动可以拆成多笔事件。
4. 如果作品已经能明确对应到某个活动，建议不要再建立独立作品事件，而是放进该活动的描述，例如：

```text
相关作品：《时间跃迁》首唱
```

5. 修改完 `data.json` 后，建议检查 JSON 是否有效：

```bash
node -e "JSON.parse(require('fs').readFileSync('data.json','utf8')); console.log('json ok')"
```

## URL 参数

网站支援以下 URL 参数：

```text
?lang=zh
?lang=tw
?lang=en
?cat=works
?q=keyword
#group-2026
```

范例：

```text
index.html?lang=zh&cat=works#group-2016-2020
index.html?lang=en&q=magazine#timelineMain
```


