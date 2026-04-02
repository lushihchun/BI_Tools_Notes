# Superset 開源版
編輯日期：2026/04/02

### 建構邏輯  
  可透過資料庫抓取資料表(Datasets)，並使用資料表建立圖表(Charts)，每個圖表只能取用一張資料表。  
  儀表板可取用圖表，同一儀表板上，即使圖表背後之資料表不同，只要置於Dimensions之欄位及值相同，圖表間都能產生交互篩選(預設全域篩選)。  
  建構圖表時，先選擇資料表，再選擇圖表類型，再將資料欄位排上圖表，後續再做圖表類型或欄位之調整。操作起來非屬探索型。
### 資料
- 由admin設定連接之database，使用者則可從database中取用datasets。
- 可接受來源(database)
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
- 圖表可調整性：高  
    - 圖表元素多數細節均可調整。
    - ※※ 只能挑選內建的系列色彩配置，不利於已有既定(或預計自訂)色彩意義的圖表陳述。
- 地圖
    - 內建15種地圖，包括最基礎的世界地圖及國家地圖(country map)。其中國家地圖包含國家邊界及第一行政區，包含台灣。
    - 使用內建地圖時，以ISO3166-2代碼對應行政區。
    - 如需要自定義地圖，可在docker中加入並修改設定以供取用。(筆者未使用過)
### 儀錶板
- 排版
    - 採橫向固定比例規格，並依縱向格線排版。
    - 採用類似flex佈局，使用互相包含的row與column控制版面。
    - 無頁籤功能，但有「段落頁籤」功能，能在單一頁面下，切換某塊內嵌之段落。
    - 在儀表板頁面變更圖表名稱，不影響原圖表。
    - 可排入標題或文字段落，但文字段落中無法取用頁面上之變數。
- 互動
    - (推測)預設所有圖表之Dimensions間都能產生交互篩選(預設全域篩選)。
### 整體操作
- 無法進行專案元素整理，但可依關鍵字搜尋。
    - 產製之圖表臚列於圖表庫，可搜尋或排序，但無法進行階層式整理。
- 圖表產製過程無複製功能，製作同類圖表需不斷重複相同動作。
- 無中文介面，但能適應瀏覽器翻譯。
### 小結
1. Superset不具資料串接及新增欄位功能，但圖表即儀表板功能強大，背後隱含的訊息即，此工具並不是被設計用於探索或分析，而是用於建構長期穩定的儀表板。  
2. 所有資料欄位的修改、分組都要回歸資料源，若資料源屬於操作上需具備IT能力的資料庫，則非常不適合推薦予非IT人員使用。  
3. 地圖內建功能完整，但如涉及自定義地圖，則需調整底層設定，非IT使用者無法使用。
4. 圖表選擇相當多，且預設外表即已相當美觀，適合建構需要吸睛的報告。  
5. 排版概念上較接近圖表網頁，整個版面屬於一個主題與網址，不會在頁面內再進行頁面的切換，只會有小區塊的切換。對於主題較大、且包含次主題較多之專案，勢必需建立成多個儀表板，建構前需想好頁面及使用規劃。另儀表板內已預設圖表互動功能，非常方便，但建構者需注意整體敘事的合理性。  
6. 整體而言，Superset偏向建構穩定儀表板的工具，不太適合用於探索及分析。非IT使用者會有非常多權限上的受限，非充實知識就能跨越，知識門檻亦高。
