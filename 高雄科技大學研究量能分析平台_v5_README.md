# 高雄科技大學研究量能分析平台 v5

## 專案說明
本平台以單一 HTML 檔呈現高雄科技大學與標竿學校的研究量能資料，涵蓋 General 總體分析、THE 學科分析、QS 學科分析、SDGs 分析與指標說明。資料期間為 2018-2025 年，並參考 `114 產學研究量能研析 20260112.pdf` 的簡報分析架構，朝向未來可由網站直接產製簡報內容。網站發布後會優先讀取同目錄的 Excel 檔案；若 Excel 讀取失敗，才使用 `index.html` 內建的備份資料。

## 主要檔案
- `index.html`：唯一保留的主要互動式網頁與 GitHub Pages 發布檔；會透過 SheetJS 自動讀取同目錄 Excel。
- `高雄科技大學研究量能分析平台_v5_README.md`：專案說明與修改紀錄。
- `00 Raw data/`：新版主要資料來源資料夾；網站會優先讀取此資料夾中的正式資料檔。
- `研究量能統計 2018-2025.xlsx`：General/THE/QS 整理後資料來源；若未放入 `00 Raw data/`，網站會 fallback 讀取 repo 根目錄同名檔。
- `00 Raw data/THE/`、`00 Raw data/QS/`：THE/QS 學科分析 SciVal raw data 資料夾；網站會依固定檔名清單讀取各學科 raw Excel，並轉成圖表所需格式。
- `00 Raw data/SDG/`：SDGs 分析資料夾，包含六校與 Taiwan 全國基準的 `Publications by SDG` 檔案，以及多校 `Summary_SDG.xlsx`。
- `00 Raw data/Collaboration/`：合作分析資料夾，放置六校國際合著與產學合著 SciVal detailed Summary 匯出檔；北科大檔名目前使用 `NTUT北科`。
- `114 產學研究量能研析 20260112.pdf`：目前網站分析架構的參考簡報。
- `教1-2.專任教師數-以「校」統計.xlsx`：教研人數資料來源。

## 維護規範
- 每次更新網站功能、版面、資料來源或發布內容時，必須同步更新本 README 的相關說明與「修改紀錄」。

## 目前版面結構
### General 總體分析
- 頁首保留「主要學校」與「年度」篩選。
- General 年度預設為目前資料中的最新數字年度，新增年度資料後會自動以最大年度作為預設；若資料中包含 `2018-2025` 這類整合期間，會保留在 General 年度篩選中。
- `主要學校年度摘要` 移至 General 的第一個區塊，桌面版摘要卡以一行五項指標呈現；每張摘要卡下方皆附該校同指標年度趨勢 sparkline，便於快速判讀長期方向。
- `趨勢指標` 選單移至 `主要學校年度摘要` 之後、年度趨勢圖之前，並納入各項論文數、FWCI 與影響力指標。
- 原本 General 最上方的 8 個 KPI 指標卡已移除，避免與年度摘要重複。
- 下方保留研究產出與研究影響力泡泡圖、當年度六校比較、滿版寬度的六校年度趨勢、合作分析摘要、六校研究量能資料表；六校年度趨勢只使用數字年度作為 x 軸，不納入 `2018-2025` 整合期間，並會依選定指標的資料範圍動態調整 y 軸、將目前篩選學校以較粗線條呈現。六校研究量能資料表另有年度篩選器，與頁首年度篩選同步連動。合作分析摘要位於六校年度趨勢之後，可切換國際合著與產學合著。資料表包含國際合著、產學合著、高被引論文與高品質期刊論文相關影響力欄位。
- 合作分析摘要已改為符合 flow 邏輯的「合作來源桑基圖」：目前情境文字顯示於 `合作類型` 篩選器旁，桑基圖本體流向為 `來源類型 → Top 5 來源項目`，節點高度與流帶寬度皆使用同一口徑的 `Total` 數值。學科領域與 Keyphrases 不再硬接入桑基圖，而是以 Top 5 摘要卡呈現；桑基圖會跟隨 General 上方 `主要學校` 篩選與合作類型同步重畫，並已拉大高度與群組間距以降低擁擠感。
- 合作分析摘要的四張 KPI 卡在桌面與平板均固定為兩欄兩列：Scholarly Output、FWCI 為第一列；Citation Count、Citations per Publication 為第二列。手機版則改為單欄，避免文字與數值擁擠。

### THE / QS 學科分析
- 保留主要學校、年度、學科領域與趨勢指標篩選。
- THE/QS 頁面的 `主要學校`、`年度`、`學科領域` 會顯示在頁面最上方同一列；`趨勢指標` 保留於 KPI 後、圖表前。
- THE/QS 的 `年度` 篩選與年度趨勢圖只顯示單一年份資料，會排除 `2018-2025` 這類整合期間選項。
- THE/QS 會優先讀取 `00 Raw data/THE/` 與 `00 Raw data/QS/` 中的 SciVal raw Excel，從檔名取得學科領域，並從 `Metric Name` 轉出 Scopus 發表數、FWCI、國際合著與產學合著相關指標；若 raw 資料夾讀不到，才使用 `研究量能統計 2018-2025.xlsx` 內的 THE/QS sheets。
- THE/QS 學校清單改為依各自資料集動態產生；QS 目前只保留 Excel QS 工作表中校名包含「科大」的 6 校資料。
- 手機版會將上述三個主篩選器改為單欄排列，避免固定三欄在窄螢幕產生水平溢位。


### SDGs 分析
- 依 PDF 第 3、4 章架構新增 `SDGs 分析` 分頁，使用 `SDG/` 資料夾內的六校與 Taiwan 全國基準 Publications by SDG 檔案，以及 `Summary_SDG.xlsx`。
- 頁面最上方提供 SDG 學校與 SDG 年度篩選；SDG項目下拉選單位於 SDGs KPI 後、重點卡片前方，列出所有 SDG 項目，預設為 SDG 1。
- 圖表包含 SDGs 整體 KPI、篩選年度校際 SDGs 發表、SDG 發表數排序、SDGs 發表數 × FWCI 影響力定位泡泡圖、目標學校最有潛力的 SDG 與 SDGs 指標資料表；`篩選年度校際 SDGs 發表` 僅比較六校，不納入 Taiwan；SDGs KPI 顯示 Scholarly Output、FWCI、Top 10% Cited、Top 10% Journals、International Collaboration 與 Citations per Publication；`SDGs目標分布`、`SDGs 重點期刊`、雷達圖、Top Keyphrases 與合作/來源摘要已移除。
- 目前多校資料包含 `Summary_SDG.xlsx` 與各校/Taiwan Publications by SDG；`目標學校最有潛力的 SDG` 直接使用 Publications by SDG 的 Scholarly Output、FWCI 與 Citation Count 計算綜合分數。Top Keyphrases 與合作/來源摘要需至 SciVal 手動取得，暫不放入 SDGs 分頁畫面。

## Excel 更新方式
- GitHub Pages 發布後，網站會自動讀取固定檔名的 Excel。新版資料統一優先放在 `00 Raw data/`。
- General/THE/QS 整理後資料建議放在 `00 Raw data/研究量能統計 2018-2025.xlsx`；若此檔不存在，網站會 fallback 讀取 repo 根目錄 `研究量能統計 2018-2025.xlsx`。
- THE/QS raw data 可分別放在 `00 Raw data/THE/`、`00 Raw data/QS/`；目前網站使用固定檔名清單讀取，若未來新增或更名學科檔案，需同步更新 `index.html` 的 `THE_RAW_FILES` / `QS_RAW_FILES`。
- SDGs 資料放在 `00 Raw data/SDG/` 子資料夾：`Summary_SDG.xlsx` 與六校/Taiwan Publications by SDG 檔案。高科大檔名為 `Publications_by_SDG_-_National_Kaohsiung_University_of_Science_and_Technology.xlsx`，Taiwan 檔名為 `Publications_by_SDG_-_Taiwan.xlsx`；Taiwan 不需另外上傳單獨的 SciVal Summary 匯出檔。
- 日後更新資料時，只要在 GitHub 上傳同名新版 Excel 覆蓋舊檔，網站重新整理後會自動讀取新版資料；`Last updated` 會依瀏覽器取得的 Excel/HTML 最後修改時間更新。
- 合作分析資料需放在 `00 Raw data/Collaboration/` 子資料夾並維持目前固定檔名；網站會讀取六校國際合著與產學合著 detailed Summary 的 Summary metrics、Keyphrase analysis 與 Top 5 合作/來源工作表。北科大可讀取 `Summary+for+NTUT北科_...` 檔名。
- `研究量能統計 2018-2025.xlsx` 需維持目前工作表名稱與欄位順序：`General`、`THE`、`QS`。
- SDGs 相關 Excel 需維持 SciVal 匯出格式與目前工作表名稱；目前網站以 `Summary_SDG.xlsx` 與各校/Taiwan Publications by SDG 更新 KPI、年度校際比較、SDG 目標分布與資料表。Top Keyphrases 與合作/來源摘要需至 SciVal 手動取得，暫不作為網站自動更新內容。
- `00 Raw data/General 2018-2025.xlsx`、`00 Raw data/FWCI_標竿學校國際合著_產學合著_高品質_高被引.xlsx` 可作為整理來源保存；目前 General 分頁仍以整理後的 `研究量能統計 2018-2025.xlsx` 為正式讀取檔，THE/QS 分頁則可直接讀取 raw folder。
- 若 Excel 暫時讀不到，網站會使用內建備份資料，避免頁面空白。
## 指標與缺值說明
- `缺值不視為 0` 的意思是：若某年度或某指標沒有資料，系統會顯示為缺值，不會把它當成 0 參與前後年度比較，以避免造成誤判。
- 目前畫面文字已調整為：`缺值會顯示為「目前缺值」，不會當作 0 計算`。
- 指標說明除了保留在 `指標說明` 分頁，也會自動套用到 KPI 標籤、摘要卡標籤與資料表欄位；滑鼠移到可辨識的指標文字上方時會顯示對應說明。

## 視覺調整
- 背景已改為深色研究文字雲風格，文字雲改為全英文並自篩選器高度附近開始散落，中央閱讀區保留乾淨空間；目前增加更多研究治理、資料、專利、永續與 AI 相關字詞，並分散於外圍背景。文字雲具備慢速漂浮、滑鼠視差與近距離跟隨互動，讓背景在不干擾閱讀的前提下保有動態感。
- Last updated 標籤改為較小字級，並放在各面板或指標卡底部。
- 前景介面已從大面積白色面板調整為深色玻璃科技風格，包含導覽列、篩選器、KPI、圖表面板、資料表與摘要卡，並同步調整圖表座標/圖例色彩以維持可讀性。
- 主標題已移除陰影與 3D 疊影，改為乾淨清晰的純文字標題。

## 修改紀錄
- 背景文字雲新增 `datasets`、`patents`、`technology transfer`、`sustainability`、`AI models`、`open access` 等研究相關字詞，並重新分散至左右與下方外圍以增加層次。
- General `六校年度趨勢` 新增動態 y 軸範圍，會依目前指標的六校年度資料自動縮放並保留上下留白，避免數值接近時折線黏在一起。
- 合作來源桑基圖加大桌面與窄螢幕顯示高度，拉開來源類型與 Top 5 來源項目的左右距離、群組間距與項目最低高度，改善標籤與流帶擁擠問題。
- 合作分析摘要的 `Top 5 Keyphrases` 卡片改為只顯示 Keyphrase 與 Relevance，不再顯示 Growth。
- 背景文字雲滑鼠互動改為近距離跟隨效果：滑鼠靠近文字時，文字會朝游標方向微幅移動，滑鼠離開視窗後回到原本漂浮位置。
- 背景文字雲新增平滑滑鼠視差互動與微幅漂浮效果，滑鼠移動時不同層級文字會以不同幅度跟隨，並保留 `prefers-reduced-motion` 使用者設定。
- 合作分析摘要調整 Sankey 呈現：`高科大｜產學合著｜2018-2025` 這類情境文字移至合作類型篩選器旁；圖內移除最左側學校節點，改由 `來源類型 → Top 5 來源項目` 呈現合作流向。
- General 年度篩選保留 `2018-2025` 整合期間資料，但六校年度趨勢與摘要卡 sparkline 改為只使用數字年度；六校研究量能資料表新增年度篩選器，並與頁首年度篩選雙向連動。
- General `主要學校年度摘要` 每張指標卡新增該校年度趨勢 sparkline；`六校年度趨勢` 將目前篩選學校線條加粗，以凸顯目標學校在校際趨勢中的位置。
- SDGs 分析中的 `SDGs 發表數比較` bar chart 補上 y 軸標題 `發表數`，讓 Scholarly Output 數值口徑更清楚。
- 網頁頁尾改為 `POWERED BY` 與 `校務大數據分析組` 兩行呈現，符合發布頁面的單位署名需求。
- THE/QS 年度篩選改為依各自資料集產生單一年份清單，排除 `2018-2025` 整合期間；THE/QS 年度趨勢圖 x 軸同步改用各自數字年份。
- 合作分析摘要改為符合桑基圖邏輯的合作來源 flow：使用 `Total` 作為唯一流量口徑，以封閉流帶呈現 `主要學校/合作類型 → Institution/Country/Author/Source → Top 5 來源項目`；學科領域改以 Scholarly Output Top 5、Keyphrases 改以 Relevance Top 5 摘要卡呈現。
- 調整合作來源桑基圖互動：取消不自然的放大動畫，改為滑鼠移入來源類型時高亮該流向、淡化其他流向。
- 指標說明新增 Scopus 每師平均、Scholarly Output、Citation Count、Citations per Publication、International Collaboration、Top 10% Cited 與 Top 10% Journals，並加入 hover tooltip，讓使用者在 KPI、摘要卡與表格欄位上可直接查看定義。
- 將合作分析正式資料移至 `00 Raw data/Collaboration/`，並支援北科大 `NTUT北科` 檔名；外層舊 `SDG/` 與 `Collaboration/` 資料夾可移除。
- THE/QS 學科分析新增 `00 Raw data/THE/` 與 `00 Raw data/QS/` raw folder parser，可從各學科 SciVal raw Excel 自動轉出網站圖表資料；主 Excel 的 THE/QS sheets 轉為 fallback。
- 網站資料讀取路徑改為優先使用 `00 Raw data/`，並保留 repo 根目錄、`SDG/`、`Collaboration/` 舊路徑 fallback；主資料檔仍需使用整理後的 `研究量能統計 2018-2025.xlsx` 格式。
- SDGs「篩選年度校際 SDGs 發表」bar chart 改為只比較六校，不納入 Taiwan 全國基準。
- General 總體分析年度預設改為依 `研究量能統計 2018-2025.xlsx` 讀入資料自動選取最大年度，避免新增年度後仍停在舊年度。
- 移除不需置入網站的 Taiwan 單獨 SciVal Summary 匯出檔；SDGs Taiwan 基準僅保留 `Summary_SDG.xlsx` 中 Taiwan rows 與 `Publications_by_SDG_-_Taiwan.xlsx`。
- SDGs 分析 KPI 新增 `Citations per Publication`，放置於 `International Collaboration` 旁邊，資料來源同為 `Summary_SDG.xlsx`。
- General「研究產出 × 研究影響力」與「六校年度趨勢」交換位置；六校年度趨勢改為滿版寬度 line chart，提升年度變化閱讀性。
- 將 General「研究產出 × 研究影響力」泡泡圖移至「合作分析摘要」之前，讓研究表現定位先於合作細節呈現。
- SDGs 分析新增 Taiwan 全國基準，會讀取 `Summary_SDG.xlsx` 中 Taiwan rows 與 `SDG/Publications_by_SDG_-_Taiwan.xlsx`，並納入 SDG 學校篩選與年度校際比較。
- 修正 THE／QS 手機版三個主篩選器的欄位覆寫規則，窄螢幕改為單欄排列，避免水平溢位。
- 重新檢視網頁版各分頁的指標區塊分配；合作分析摘要改用專用雙欄 KPI 網格，四項指標固定呈現為 2 × 2，避免桌面版出現 3 + 1 的不均衡排列。
- 修正合作分析摘要的合作類型切換事件，切換國際合著／產學合著時會立即重畫摘要；合作分析摘要移至 General「六校年度趨勢」之後。
- 將 SDG項目 下拉選單移至 SDGs KPI 後、Scholarly Output／FWCI／Citation Count 重點卡片上方。
- 新增維護規範：日後每次網站更新皆須同步更新本 README 的相關說明與修改紀錄。
- 強化合作分析摘要篩選：合作類型下拉選單改為直接重畫合作摘要，避免切換國際合著/產學合著時畫面未更新。
- 修正預設與篩選：主要學校預設高科大，年度與 SDG 年度預設最新年度；合作分析摘要的合作類型篩選正常初始化；SDG 篩選標籤改為 `SDG項目` 並預設 SDG 1。
- 將學校代表色調深並降低亮度，使 General、THE、QS 與 SDGs 校際比較圖表更貼合深色科技感背景。
- SDG 重點卡片的排名說明改為明確標示「在該校各 SDG 目標中」依 Scholarly Output 或 FWCI 排名，避免誤解為校際排名。
- 合作分析摘要新增學科領域分布，依 Scholarly Output 由多到少上下排序；SDG detailed Summary 的 subject area 資料也同步改為由多到少排序。
- General 總體分析新增「合作分析摘要」，自動讀取 `Collaboration/` 內六校國際合著與產學合著 SciVal detailed Summary，呈現 KPI、學科領域分布、Top Keyphrases 與合作/來源摘要；學科領域分布依 Scholarly Output 由多到少排列。
- SDGs 分析將「篩選年度 SDGs 發表表現」改名為「篩選年度校際 SDGs 發表」；「SDGs 學科領域分布」改為使用 Publications by SDG 的「SDGs目標分布」doughnut chart，並先移除 Top Keyphrases 與合作/來源摘要面板。
- 依 研究量能統計 2018-2025.xlsx 的 Scource 工作表更新指標說明：國際合著改為 international co-authorship，產學合著明確標示 corporate sector，並補充高被引/高品質期刊 FWCI 定義。
### 2026-07-16
- SDGs 分析移除上方 Total Citation Count KPI 與雷達圖，改以篩選年度六校 SDGs Scholarly Output bar chart 呈現；高科大 detailed subject/keyphrase/partner 備份資料恢復顯示，其他學校若無 detailed Summary 匯出檔會顯示缺資料提示。
- 背景文字雲加入 `notranslate`、`translate="no"` 與 `lang="en"` 標記，避免同事瀏覽器自動翻譯時將背景英文關鍵字翻成中文。
- 釐清 SDGs KPI 口徑：Scholarly Output、FWCI、Top 10% 與 International Collaboration 來自 `Summary_SDG.xlsx`；上方 Total Citation Count KPI 已移除，避免與 Publications by SDG 累計引用數混淆。
- SDGs 分析調整為學校、年度、SDG項目 篩選置頂；SDG項目 改列所有 SDG 項目，KPI 可依 `Summary_SDG.xlsx` 切換 Overall/2018-2025 年度，SDG 圖表改用聯合國官方色並移除 `SDGs 重點期刊` 圖表。
- 放大整體介面字級，包含導覽按鈕、篩選器、KPI、摘要卡、表格、說明文字與 Chart.js 圖例/座標/tooltip 文字，提升一般瀏覽器閱讀性。
- 將 General、THE、QS 圖表中的 line/bar/bubble 視覺色彩調整為較柔和的馬卡龍色系；SDGs 圖表維持聯合國 SDG 目標官方色。
- SDGs 分析改為讀取 `SDG/` 子資料夾的多校資料，新增 `SDG 學校` 篩選，並補入 NKUST Publications by SDG 正式檔名；舊的根目錄 NKUST SDG 檔將不再作為網站讀取來源。
- 網站改為優先讀取同目錄 Excel 檔案，支援 GitHub 上傳同名新版 Excel 後自動更新圖表與資料表；.gitignore 同步改為允許正式 Excel 檔上傳。
- SDGs 分析新增 SDG 目標官方色系，並移除頁首主標題陰影。
- `主要學校年度摘要` 桌面版改為一行五項指標；General `趨勢指標` 補上國際/產學合著論文數、FWCI、影響力，以及高被引/高品質論文數與 FWCI。
- 文字雲垂直位置下移，改為從篩選器高度附近開始分布；General 頁的 `主要學校` 與 `年度` 主控恢復兩欄置中，THE/QS 則維持三欄主控。
- THE/QS 的 `學科領域` 篩選改與 `主要學校`、`年度` 放在最上方同一列，讓主控篩選更集中。
- 文字雲背景改為避開中央標題、按鈕與內容區，關鍵字全數改為英文，並細修玻璃面板、按鈕陰影與背景格線以提升整體質感。
- 背景由漂浮工程/幾何物件改為研究文字雲風格，移除原本 SVG 研究物件底圖，改用關鍵字大小層級呈現研究主題。
- 背景新增更多漂浮幾何圖形與研究工作物件，包含菱形框、軌道、長條圖、筆電、論文頁與筆。
- 導覽列 3D 按鈕加大尺寸，提升一般瀏覽器版面的辨識度。
- THE/QS 上方六個 KPI 指標卡改為桌面版 3 欄排列，形成三個一組、兩排顯示。
- 調整頁首主標題 3D 陰影與發光強度，讓「高雄科技大學研究量能分析平台」文字更清晰銳利。
- 刪除原本的中文命名 HTML 檔，專案改為僅保留 `index.html` 一份作為維護與發布檔。
- 背景幾何圖形強化，新增漂浮三角線框、節點網絡與斜向資料平面。
- THE/QS 學科分析頁將 `主要學校`、`年度`、`學科領域` 移至頁面最上層同一列，`趨勢指標` 保留於圖表前方。
- 導覽列取消整條背景帶，改為四個 3D 立體按鈕；頁首標題加入 3D 立體字效果。
- 依前景白色面板突兀問題，將導覽列、篩選器、KPI、圖表面板、資料表與摘要卡調整為深色玻璃科技風格，並同步調整圖表座標/圖例色彩以維持可讀性。
- THE/QS 學科分析篩選器改為顯示在各自頁面 KPI 後、圖表前，讓篩選器緊接相關圖表。
- `Last updated` 改為依瀏覽器取得的 HTML 檔案最後修改時間自動顯示，不再手動固定日期。
- 背景物件改為多個分離透明 PNG，分散在背景並加入緩慢漂浮動畫，呈現無重力空間感。`船舶` 與 `模具齒輪` 已重新拉開位置，並加入半透明 3D 幾何環、方塊與資料格線作為背景層。
- 指標說明移除「資料取得方式：參考教學影片。」文字。
- 背景改用 AI 生成的透明 PNG 3D 物件圖，納入工科、海洋、商管、機械與模具元素。
- 六校研究量能資料表新增國際合著論文影響力、產學合著論文影響力、高被引論文FWCI 與高品質期刊論文FWCI 欄位。
- 強化深色背景中的研究物件辨識度，加入較明顯的顯微鏡、燒瓶/試管與 DNA/分子圖形。
- 依發布前視覺調整需求，將背景改為較深色的 3D 研究物件與資料平台風格。
- 發布前再次調整背景，改為更低調、正式的研究資料平台視覺。

### 2026-07-15
- 將 General 的 `主要學校年度摘要` 移至頁面最前方。
- 移除 General 頁面頂端 8 個 KPI 指標卡。
- 將 `Last updated` 改為小型底部標籤。
- 將 `缺值不視為 0` 改寫為更清楚的說明文字。
- 將背景改為 3D 專業研究資料風格。
- 將 General 的 `趨勢指標` 選單移至 `主要學校年度摘要` 後方；THE/QS 仍保留上方趨勢指標選單。
- 依使用者更新後的 Excel `QS` 工作表重新匯入 QS 學科分析資料，僅保留校名包含「科大」的 210 筆資料。
- 建立並確認發布用 `index.html`，內容與主 HTML 檔一致。
- 初始化本機 Git repository，並加入 `.gitignore` 排除 Excel 原始資料與暫存檔，準備使用 GitHub Pages 發布。
- 修正 THE/QS 學科分析的圖表與資料表學校清單邏輯，改為依 THE/QS 各自資料集顯示，而不是固定使用 General 六校清單。

## 發布建議
此專案是靜態 HTML，可使用 GitHub Pages 或其他靜態網站平台發布。目前僅保留發布用 `index.html`，避免維護兩份 HTML 造成版本混淆。

可用的發布方式包含：
- GitHub Pages
- Netlify / Vercel / Cloudflare Pages
- 自有伺服器或 NAS
- 區網內以本機 Web server 方式分享

若使用 GitHub Pages，將 `index.html` 放在 repo 根目錄後，於 repository 的 Settings > Pages 啟用 main branch / root 目錄部署即可。
