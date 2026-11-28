# 口說備忘：Software Engineering · Testing & Simulation · LLM Serving Optimization

投影片共 13 張（10 張主講，含結尾；3 張問答備用）。英文投影片搭配繁體中文口說稿。研究正式題目為 **Carbon- and Power-Aware Multi-Tier KV Cache Management for Heterogeneous GPU LLM Serving**，範圍是單一伺服器內的異質 GPU 推論系統。

## 時間配置

完整主講約 **7–8 分鐘**，LLM 研究段約 **3 分鐘**。下表是排練目標；依面試官背景，可縮短案例或補充技術備註。備用投影片供問答使用，不計入主講時間。

| 張 | 主題 | 目標時間 |
| --- | --- | --- |
| 1 | 封面 | 10 秒 |
| 2 | 學經歷 | 30 秒 |
| 3 | NeoPower 系統架構 | 50 秒 |
| 4 | NeoPower 情境模擬 | 80 秒 |
| 5 | NeoPower 部署前後驗證 | 70 秒 |
| 6 | 異質 GPU LLM Serving | 45 秒 |
| 7 | 細粒度效能與功耗建模 | 45 秒 |
| 8 | 系統級模擬研究方法 | 50 秒 |
| 9 | 效能限制下的資源最佳化 | 40 秒 |
| 10 | 結語 | 10 秒 |

## 第 1 張 — Software Engineering & System Simulation

目標時間：15 秒。

各位好，我是 Yu-Jui Liang。今天介紹我在 NeoPower 的後端開發、系統模擬與測試經驗，以及目前進行中的異質 GPU LLM Serving 資源管理研究。

學歷留到下一頁，不重複介紹。

## 第 2 張 — Education & Professional Experience

目標時間：35 秒。

我目前就讀臺大資料科學碩士學位學程，預計 2027 年 6 月畢業。大學就讀政大資訊科學系，雙主修電子物理。

工作方面，我曾在英業達集團的 AIMobile，以及 NeoPower 擔任約聘軟體工程師。接下來主要介紹 NeoPower 的工作，聚焦在後端系統、我開發的模擬器，以及部署前後的驗證。

保留原有學經歷，不展開其他專案。

## 第 3 張 — NeoPower: Backend System Architecture

目標時間：50 秒。

NeoPower 新動智能是一間做電動車能源管理的新創。我從大二加入，一直工作到大四。公司開發的是電動巴士充電管理平台，需要整合車輛、充電設備與外部廠商。

我的工作包含系統規劃與軟體開發、後端 API、資料庫整合、系統日誌分析與除錯，也參與部分部署、維運及維護。

圖中一個重要考量是容器隔離。公司的伺服器同時執行不同專案與客戶的服務，我們透過容器隔離服務和執行環境，讓部署、除錯與排查更容易，也減少對其他正式系統的干擾。

延伸與界線：

- 架構圖呈現平台關係，並不表示整套平台都是我獨自設計。
- 容器隔離的重點是共用伺服器上的服務管理，不宣稱完全消除效能或資源干擾。
- 10 分鐘版可沿前端、後端、資料庫與外部廠商走一次互動，再說明隔離如何協助排查。這頁不展開回歸測試。

## 第 4 張 — NeoPower: Scenario-Based System Simulation

目標時間：90 秒。NeoPower 段的重點頁。

另一項重要工作，是我親自開發了一個自訂系統模擬器，用來測試軟體、除錯和重現錯誤。

平台需要與車載系統和充電設備等多家外部廠商互動。開發時不能反覆呼叫廠商的正式系統，也不能每次重現故障都要求對方配合。因此，我開發模擬器來重現外部廠商的行為；依整合情境，廠商可能扮演 client，也可能扮演 server。這樣就能在本地、可控制的條件下驗證系統。

情境不是隨意編出來的。我們參考正式資料庫裡的歷史日誌、客戶回饋與抱怨，以及過去觀察到的營運問題，定義需要重現的流程與錯誤，再透過模擬器與被測後端互動，檢查行為。

兩個代表例子是：很多公車同時進站，充電需求和系統負載快速上升；以及網路設備故障，造成多個充電站或充電樁同時斷線，讓後端必須處理大量異常事件。

模擬器可以支援功能測試、除錯、錯誤重現與回歸測試。下一頁說明這些測試如何用在部署前後。

延伸與界線：

- 圖中的 client／server 是模擬器可重現的廠商角色，不是額外使用第三方模擬器的主張。
- 10 分鐘版可各用一小段說明兩個代表情境如何從歷史資訊形成案例；不編造協定、事故編號、負載數字或效能改善。
- 模擬涵蓋選定的工作流程與異常條件，不能據此宣稱與所有真實設備完全等價。

## 第 5 張 — NeoPower: Testing & Production Reliability

目標時間：80 秒。

我們在開發或修改功能之後，會先用模擬器驗證相關的正常和異常條件，也做回歸測試，確認既有功能沒有被破壞。必要的部署前測試都通過，才能將更新後的系統部署上線。

上線後還要做驗證。一個例子是充電功率分配演算法：系統依不同車輛的充電需求，分配可用功率。新演算法開發後，可以與原本的版本比較實際運作行為。

我們採用的方法之一，是選擇營運條件相近的充電站。有些站使用舊演算法，另一些站使用更新後的演算法，再收集兩邊的營運資料。

接著一起分析系統日誌、實際營運數據與客戶回饋，判斷新演算法是否達到預期改善，以及是否滿足客戶需求。左邊確認變更可以上線，右邊確認上線後在實際環境的表現。

技術備註與問答：

- 跨站比較是觀察性驗證，不是隨機對照實驗。站點、車流與營運條件仍可能有差異，不能僅憑比較就推論因果或統計顯著。
- 10 分鐘版多說如何將日誌、營運資料與回饋一起判讀，以及條件相近仍有上述限制。
- 本簡報不提供未確認的改善比例或實驗結果，也不延伸其他時間分組方法。

## 第 6 張 — Heterogeneous GPU LLM Serving

目標時間：45 秒。

我的碩士研究正式題目是 Carbon- and Power-Aware Multi-Tier KV Cache Management for Heterogeneous GPU LLM Serving。目前的範圍是單一伺服器內有多種 GPU 的 LLM 推論環境。請求進入 Serving Engine，由 Request Scheduling 與 Continuous Batching 管理，再由異質 GPU 執行。

研究關注 KV Cache 在 GPU 本地 HBM、共享 Host DRAM 和 SSD 之間的配置、搬移、暫存與還原。這些層級在容量、頻寬、存取延遲、功耗與能效上不同，GPU 也可能有不同的運算吞吐量。圖是概念性的研究架構，不代表已完成實作；箭頭只表示資料搬移概念，不假設特定的實體互連拓樸或 GPU 直接存取 SSD 能力。

目標是在符合 Serving 效能要求下提升能源效率並降低碳排。這些仍是研究目標，尚無實驗結果。

## 第 7 張 — Fine-Grained Performance & Power Modeling

目標時間：45 秒。

要比較不同 GPU 和快取配置，首先需要掌握不同推論工作在硬體上的時間與能耗。這裡將模型分成四類：Prefill Attention、Prefill FFN、Decode Attention 和 Decode FFN。Attention 與 FFN 在這裡是建模分類，並不是要把它們部署成分離的 GPU Worker。

建模會考慮 GPU 運算吞吐量、記憶體頻寬與容量、Batch Size、Sequence Length 和工作負載特徵，預期估計輸出是 Latency（毫秒）、Power（瓦特）與 Energy（焦耳）。Hardware Profiling、模型建構、Calibration 與 Validation 都是接下來要做的研究工作，目前沒有宣稱已完成或驗證模型。

## 第 8 張 — Research Methodology: System-Level Simulation

目標時間：50 秒。

接著把 GPU、記憶體／儲存和工作負載模型放進 System-Level Discrete-Event Simulator。輸入包含 GPU 的運算、延遲、功率與能量模型；HBM、DRAM、SSD 的容量、頻寬、存取延遲和 I/O；以及請求到達、輸入輸出 Token 長度、KV Cache 重用和 Batching 機會。

模擬器預計處理 Request Scheduling、Continuous Batching、GPU 執行、記憶體配置、多層 KV 管理、儲存 I/O、資料搬移、佇列和資源競爭。之後評估 TTFT、TPOT、Throughput、Goodput、平均和尖峰功率、系統能耗，以及 Operational Carbon 與 Allocated Embodied Carbon。Goodput 是符合定義服務目標的成功請求率。

研究會評估及重用開源模擬框架、硬體 Profiling 資料和既有建模方法。Hardware Benchmarking、Model Calibration 與 Validation 是校準模型的規劃環節。這是提議中的系統架構；整合和驗證仍在規劃或進行中，並非 GPU Cycle-Accurate Simulation。

## 第 9 張 — Performance-Constrained Resource Optimization

目標時間：40 秒。

預計探索的變數包括 DRAM 和 SSD 的邏輯快取容量、不同群組的 TTL、快取放置與保留政策，以及還原快取或重新計算的選擇。這些是既有硬體上的邏輯資源配置，不代表會因此減少已安裝硬體或製造階段的碳排。

最佳化目標會考慮系統能耗、Operational Carbon、Allocated Embodied Carbon，以及平均和尖峰功率；同時受 TTFT、TPOT、Required Goodput、Power Budget 和容量限制。Operational Carbon 取決於用電量與電力碳強度；Embodied Carbon 分攤是帳務估算，不能解讀成實際減少硬體製造排放。能源歸因也要避免不同元件重複計算。

這頁的核心問題是：KV Cache Hit Rate 越高，系統能耗就一定越低嗎？重用快取可能省下重複運算，但保留快取、Storage I/O 和資料搬移也會消耗能量。這是要用可比較的工作負載、完成服務量與相同效能限制驗證的研究問題，不是已得到的結論。

目前完成初步文獻整理、研究問題定義和初步框架分析；正在設計建模架構、評估框架可行性與規劃實驗。接下來是重現 Baseline、硬體 Profiling、模型 Calibration / Validation，以及資源最佳化實驗。

## 第 10 張 — Thank You

目標時間：10 秒。

NeoPower 的經驗讓我實際參與軟體開發、系統模擬、測試與驗證；接下來我希望把這些 Systems Engineering 經驗用在 LLM Serving，透過硬體特性分析、效能模型與系統模擬研究資源管理。謝謝各位，歡迎提問。

## 備用投影片 — Slides 11–13

第 11 張 SAT-LEX 說明如何把法律文件轉成 SMT Constraints、把報告或情境轉成 Logical Variables，再用 SMT Solver 檢查一致性。第 12–13 張是 ABC Technology Mapping 的備用內容，可在面試官詢問 EDA 專案時使用。三張備用頁不計入主講時間。
