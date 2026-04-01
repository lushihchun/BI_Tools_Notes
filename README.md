# BI_Tools_Notes
編輯時間：2026/4/1

## Metabase 開源版
### 建構邏輯  
  以「提問」為基本單位，一個提問內含一串資料處理過程及一份產出的視覺化圖表，所有資料的串階及處理皆係於各個提問下獨立進行。  
  儀錶板中排入各個「提問(圖表)」後，由使用者自行在儀表板介面中，手動設定各圖表或篩選器內資料欄的關係，達到互動篩選效果。  
  建構提問(圖表)時，可先選擇圖表上要放的資料，再到可視化頁面挑選圖表，不須一開始就決定好圖表類型。
### 資料
- 可接受來源  
      MySQL、PostgreSQL、SQLServer、Amazon Redshift、BigQuery、Snowflake、Amazon Athena、ClickHouse、Detabricks、Druid、DruidJDBC、MongoDB、Presto、SparkSQL、SQLite、Starburst
- 資料表之串接&新增欄位功能  
    - 內建基礎資料處理功能，可用點選方式，進行新增自訂欄位、資料表間的欄位串接，及資料預篩選等，並儲存於提問中。
    - 自訂欄位部分，提供數十個基礎函式協助資料處理。
    - 提供資料「模型」功能：從資料庫資料進行預處理(類似view)，供後續提問(圖表)取用。
- 語言  
  使用繁體中文未遇困難。
###  圖表
- 圖表種類  
    - 基本款完備，包括：表格、柱狀圖(直/橫)、折線圖、圓餅圖、面積圖、組合圖、地圖、散點圖、瀑布圖、數字卡、透視表、趨勢數字卡、量測計卡、進度卡(達標標示)、漏斗圖、桑基圖
- 圖內運算  
    - 基本款完備，包括：總行數、總和、平均、中位數、不重複值總數、累積和、累積行數、標準差、最小值、最大值
    - 在特定圖表中可自行計算百分比(eg.堆疊百分比長條圖、圓餅圖等)。
- 圖表可調整性：中等  
    - 可調整圖表元素之顯示與否，但無法調整細節。如：可決定是否顯示x軸，但無法控制刻度粒度；可決定是否顯示圖例，但無法決定圖例位置。
    - 可在既有色卡內自行調整顏色配置。
- 地圖  
    - 可於系統管理者權限下使用geojson自定義地圖，惟geojson檔須為網路連結(不提供上傳功能)。
    - 地圖檔中須包含geojson地理資料及區塊標籤。每張地圖僅能選一欄標籤作為對外串接之依據。
    - 目前嘗試下，只能以一項連續數值描述區域地圖(5階顏色深淺)。
### 儀錶板
- 排版
    - 可選固定寬度(長形網頁寬度)或全螢幕(橫向固定比例)規格。
    - 依橫向及縱向格線排版。
    - 具頁籤功能，同一網頁下可依不同次主題切換頁面。
    - 圖表(提問)在儀表板頁面可做小幅度的外觀變更(eg表頭名稱)，不影響原圖表。
- 互動
    - 無預設。使用者可於儀錶板介面手動設定篩選器或圖表間之關聯。
### 整體操作
- 可進行專案元素整理
    - 所有的提問及儀表板均可透過文件夾進行整理。
    - 需進行相同資料處理的同類提問(圖表)，可直接「複製提問」後另存，再進行內容修改，操作上更為便利且能確保邏輯一致。(但無法批次複製)
- 具中文介面易於使用。
### 小結
  具備資料串接及簡易自訂欄位功能，方便探索過程反覆修改及操作。  
  不提供太花俏的圖表，但各種表達都有圖可用；不給使用者調整細節的外觀，但關鍵功能(eg圖表顏色)仍有給予彈性。預設外觀足夠美觀，不會讓使用者有急於調整的需求。  
  圖表的製作邏輯以很明確的方式記錄並呈現在後台，易於理解、修改及檢討，並具備圖表(提問)整理的功能，便於專案管理。  
  未預設儀表板中各圖表的關係， 感覺不如其他BI工具智慧，但圖表間關係邏輯更清楚。  
  對於有操作BI工具經驗者，多數的功能都能自己摸索找到，並在操作過程中自行理解設定方式，不須一直查詢，符合使用者直覺。  
  整體而言，圖表變化性不大但務實功能上相當夠用，而且在美觀上相當省力，除非使用者有較花俏的圖表需求(eg雷達圖)，不然頗適合推薦給非IT分析人員，但操作上仍須事前具備基本的圖表與資料概念。  
  
---
## Superset 開源版
### 建構邏輯  
  可透過資料庫抓取資料表(Datasets)，並使用資料表建立圖表(Charts)，每個圖表只能取用一張資料表。  
  儀表板可取用圖表，同一儀表板上，即使圖表背後之資料表不同，只要置於Dimensions之欄位及值相同，圖表間都能產生交互篩選(預設全域篩選)。  
  建構圖表時，先選擇資料表，再選擇圖表類型，再將資料欄位排上圖表，後續再做圖表類型或欄位之調整。操作起來非屬探索型。
### 資料
- 由admin權限者設定連接之database，使用者權限者只能從database中取用datasets。
- 可接受來源database
    - 須預先於docker中安裝該類資料庫之驅動程式。可安裝之資料庫包括：https://superset.apache.org/user-docs/databases/ (撰寫時約80種，包括googlesheet)。
- 資料表之串接&新增欄位功能
    - 無法於Superset中進行資料表處理，包括串接及新增欄位。
    - 需於資料庫中串接好並完成欄位處理，再存成資料表(或view)，後由Superset取用。資料表於資料庫中更新時，Superset中備有更新資料源功能，無須刪除再重讀。
- 語言
    - 中文部分，需使用UTF-8(SQL Server之欄位需為NVARCHAR非VARCHAR)，方不會出現亂碼。
###  圖表
- 圖表種類
    - 50餘種：Area Chart、Bar Chart、Big Number、Big Number with Trendline、Box Plot、Bubble Chart、Bubble Chart (legacy)、Bullet Chart、Calendar Heatmap、Cartodiagram、Chord Diagram、Country Map、deck.gl 3D Hexagon、deck.gl Arc、deck.gl Contour、deck.gl Geojson、deck.gl Grid、deck.gl Heatmap、deck.gl Multiple Layers、deck.gl Path、deck.gl Polygon、deck.gl Scatterplot、deck.gl Screen Grid、Funnel Chart、Gantt Chart、Gauge Chart、Generic Chart、Graph Chart、Handlebars、Heatmap、Histogram、Horizon Chart、Line Chart、MapBox、Mixed Chart、Nightingale Rose Chart、Paired t-test Table、Parallel Coordinates、Partition Chart、Pie Chart、Pivot Table、Radar Chart、Sankey Chart、Scatter Plot、Smooth Line、Stepped Line、Sunburst Chart、Table、Time-series Percent Change、Time-series Period Pivot、Time-series Table、Tree Chart、Treemap、Waterfall Chart、Word Cloud、World Map
- 圖內運算
    - 包括：AVG、COUNT、COUNT_DISTINCT、MAX、MIN、SUM
    - 在Part of a Whole圖表群中可自行計算百分比(eg.圓餅圖、樹狀圖等)。
- 圖表可調整性：
- 地圖  
### 儀錶板
- 排版
- 互動
### 整體操作
- 可進行專案元素整理
- 具中文介面易於使用。
### 小結
