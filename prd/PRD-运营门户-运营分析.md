# 需求文档 - 运营分析

## 1. 功能概述

- 1.1 功能名称：运营分析
- 1.2 功能概述：运营分析模块旨在基于适配中心汇集和管理的各类数据（包括客户数据、设备数据、业务数据等），提供多维度的统计分析能力。通过图表化展示和报表导出等功能，帮助运营人员洞察客户行为特征、评估设备资源效益、监控业务发展态势，从而为精细化运营、资源优化配置和业务决策提供数据支持。

## 2. 用户与场景

- 2.1 目标用户: 省级适配中心运营人员、业务分析师、运维管理人员、管理决策层。
- 2.2 用户场景/故事:
    - 场景一：作为一个省级适配中心运营经理，我想要按区域、行业等维度查看客户数量分布及活跃客户占比，以便了解不同客户群体的构成和参与度，为市场推广和客户维系策略提供依据。
    - 场景二：作为一个省级适配中心运维主管，我需要分析接入设备的厂商分布、在线率、故障频率以及视频流的平均利用率，以便评估设备健康度和资源使用效率，指导运维工作的优化和资源调整。
    - 场景三：作为一个省级适配中心业务分析师，我希望能统计各类视频业务（如点播、回放）的使用总量、并发峰值及时段分布，并分析其增长趋势和用户偏好，以便发现热门应用场景，支持新业务的规划和现有业务的迭代优化。
    - 场景四：作为一个省级适配中心管理人员，我需要定期导出客户分析、设备分析和业务分析的报表，以便于进行月度/季度回顾、编写运营报告和向上级汇报。

## 3. 功能范围/列表

- 3.1 功能模块一: 客户分析
- 3.2 功能模块二: 设备分析
- 3.3 功能模块三: 业务分析

## 4. 功能模块详情

---

### 4.1 功能模块：客户分析

#### 4.1.1 功能描述与目标

- 解决的问题: 运营团队需要深入了解其服务的省内客户群体的具体构成、活跃情况、资源使用习惯以及潜在价值，以便进行更精准的客户分层、服务和营销。
- 用户价值/目标: 通过多维度的数据分析，清晰描绘客户画像，识别高价值客户与流失风险客户，优化客户服务策略，提升客户满意度和业务收入。
- 核心能力概述: 基于适配中心管理或同步的客户数据，提供多维度分析能力，例如：按区域、行业、客户级别统计客户数量与分布情况；分析活跃客户数量、非活跃客户占比；统计客户平均资源使用量（如视频路数）；并可结合业务数据进行客户价值分析等，支持图表化展示和报表导出。 
    

#### 4.1.2 原型参考

- 主要原型页面: 运营分析原型.html - 客户分析标签页

#### 4.1.3 详细需求

##### 4.1.3.1 功能入口与触发条件

- 入口: 运营门户模块 -> 运营分析 -> 客户分析 [参考原型 运营分析原型.html - 客户分析标签页]
- 触发条件: 用户已登录，并拥有“客户分析”功能的查看权限。

##### 4.1.3.2 交互流程与界面详述

- **A. 客户分析看板** [参考原型 运营分析原型.html - 客户分析标签页]
    - 布局: 顶部为筛选条件区（时间范围、所属行业、客户级别、所属区域四个筛选器），中间为关键指标卡片区（4个指标卡片横向排列），下方为图表区域（2x2网格布局展示4个分析图表）。
    - **数据维度 (可用于筛选和分组统计)**:
        - 时间维度: 日、周、月、季度、年，或自定义时间范围。
        - 所属区域: 华北、华东、华南、华中、西南、西北、东北。
        - 所属行业: 政府机关、教育、医疗、金融、制造业。
        - 客户级别: 战略客户、重要客户、普通客户。
        - 客户来源: 如CRM同步、手动创建。
        - 客户状态: 如活跃、非活跃、即将流失（活跃度需定义规则）。
    - **关键指标卡片展示**:
        - 客户总数卡片: 显示客户总数（如1248），包含较上月增长百分比（如+12.5%）。
        - 活跃客户卡片: 显示活跃客户数（如986），包含活跃率百分比（如79.0%）。
        - 平均资源使用量卡片: 显示平均资源使用量（如15.6个/客户）。
        - 客户价值评分卡片: 显示客户价值评分（如8.2平均分）。
    - **图表区域展示**:
        - 客户行业分布图: 饼图展示不同行业客户数量占比。
        - 客户增长趋势图: 折线图展示客户数量随时间变化趋势。
        - 客户级别分布图: 柱状图展示不同级别客户数量分布。
        - 客户活跃度分析图: 组合图表展示客户活跃度相关指标。
    - **交互功能**:
        - 筛选器: 用户可选择不同维度组合进行数据筛选和下钻。
        - 图表联动: 点击某一图表中的分类，其他相关图表可联动刷新数据。
        - 数据提示: 鼠标悬浮在图表元素上时，显示详细的数据值和说明。
        - 时间范围选择: 支持选择预设的时间范围（如近7天、近30天、本月、本年）或自定义起止日期。
- **B. 报表导出**
    - 触发: 在客户分析看板页面，提供“导出报表”按钮。
    - 交互步骤:
        - Step 1: 用户点击“导出报表”按钮。
        - Step 2: 系统可提供选项，允许用户选择导出当前看板视图（所见即所得的截图或PDF），或导出明细数据/汇总数据。
        - Step 3: 选择导出格式（如CSV、Excel、PDF）。 
            
        - Step 4: 系统后台生成报表文件并提供下载。对于大数据量导出，可采用异步生成并通过消息通知用户下载。

##### 4.1.3.3 数据定义 (分析维度与指标)

- **分析维度**: 见4.1.3.2 A. 数据维度部分。包括时间、地理区域、所属行业、客户级别、客户来源、客户状态等。
- **关键指标**: 见4.1.3.2 A. 关键指标与可视化展示部分。包括客户总数、各分类客户数及占比、活跃/非活跃客户数及占比、平均资源使用量、客户价值评分等。

##### 4.1.3.4 权限控制

- 功能访问权限: 拥有“客户分析-查看”权限的用户可以访问客户分析看板。
- 报表导出权限: 可设为与查看权限相同，或单独控制“客户分析-导出”权限。

#### 4.1.4 业务规则

- 数据来源: 客户分析的数据主要来源于适配中心的客户信息管理模块（包括手动录入和CRM同步的客户数据）以及客户资源授权管理模块的数据。活跃度、价值分析等可能需要结合业务日志或（省侧）业务分析模块的数据。
- 指标计算规则:
    - 活跃客户定义: 需明确定义活跃客户的标准，例如“在过去30天内至少有一次视频调阅行为的客户”或“当前有生效中资源授权的客户”。此规则应可由管理员在后台配置或系统预设。
    - 非活跃客户占比: (总客户数 - 活跃客户数) / 总客户数 * 100%。
    - 客户平均资源使用量: 特定资源总使用量 / 客户总数（或活跃客户数，需明确）。
- 数据更新频率: 分析看板的数据应定期更新，例如每日凌晨进行ETL处理和汇总计算。部分关键实时指标可支持更高频率的刷新。
- 历史数据保留: 运营分析模块应能支持对一定时间跨度（如过去1-3年）的历史数据进行分析。

#### 4.1.5 异常处理方案

- 数据为空或不足: 当筛选条件下无数据或数据量过少不足以生成有效分析图表时，界面应友好提示“暂无数据”或“数据量不足，无法生成分析图表”。
- 图表加载失败: 若因网络问题或后端服务异常导致图表无法加载，应显示加载失败的提示，并可尝试提供手动刷新按钮。
- 报表导出超时或失败: 对于大数据量的报表导出，若处理时间过长，应有进度提示或转为异步任务。若导出失败，应提示用户失败原因（如系统错误、无权限等）。

#### 4.1.6 与其他功能的关联和依赖

- **依赖项 (Dependencies)**:
    - 客户信息管理模块: 提供客户的基础信息和分类属性数据。
    - 客户授权资源管理模块: 提供客户的资源授权和使用数据。
- **被依赖项 (Generated Dependencies)**:
    - 无直接被其他功能模块强依赖，其产出的分析结果主要供人工决策和制定运营策略。

---

### 4.2 功能模块：设备分析

#### 4.2.1 功能描述与目标

- 解决的问题: 运维和运营团队需要全面了解通过适配中心接入的各类省级设备的数量分布、运行状态、故障情况以及资源利用效率，以便进行有效的设备管理、故障预警和资源优化。
- 用户价值/目标: 提升设备运维效率，保障设备运行稳定性，优化设备资源配置，降低运维成本，并为设备采购和升级提供数据支持。
- 核心能力概述: 针对通过适配中心接入的省级设备，进行多维度统计分析，例如：按设备厂商、型号、所属省级平台、接入区域统计设备数量和分布；分析设备在线率、离线时长、故障发生频率；评估设备视频流平均利用率、存储资源占用情况等，帮助优化资源配置和运维策略。 
    

#### 4.2.2 原型参考

- 主要原型页面: 运营分析原型.html - 设备分析标签页

#### 4.2.3 详细需求

##### 4.2.3.1 功能入口与触发条件

- 入口: 运营门户模块 -> 运营分析 -> 设备分析 [参考原型 运营分析原型.html - 设备分析标签页]
- 触发条件: 用户已登录，并拥有“设备分析”功能的查看权限。

##### 4.2.3.2 交互流程与界面详述

- **A. 设备分析看板** [参考原型 运营分析原型.html - 设备分析标签页]
    - 布局: 顶部为筛选条件区（时间范围、设备厂商、设备平台、所属区域、设备状态五个筛选器），中间为关键指标卡片区（4个指标卡片横向排列），下方为图表区域（2x2网格布局展示4个分析图表）。
    - **数据维度 (可用于筛选和分组统计)**:
        - 时间维度: 日、周、月、季度、年，或自定义时间范围。
        - 设备厂商: 海康威视、大华、华为、宇视、科达。
        - 设备平台: 国标平台、私有平台、云平台。
        - 所属区域: 华北、华东、华南、华中、西南、西北、东北。
        - 设备状态: 在线、离线、故障。
    - **关键指标卡片展示**:
        - 设备总数卡片: 显示设备总数（如3456），包含较上月增长百分比（如+8.3%）。
        - 在线率卡片: 显示设备在线率（如95.2%），包含在线设备数量。
        - 平均离线时长卡片: 显示平均离线时长（如2.3小时）。
        - 视频流利用率卡片: 显示视频流利用率（如78.5%）。
    - **图表区域展示**:
        - 设备厂商分布图: 饼图展示不同厂商设备数量占比。
        - 在线率趋势图: 折线图展示设备在线率随时间变化趋势。
        - 故障分析图: 柱状图展示设备故障类型和数量分布。
        - 资源利用率图: 组合图表展示设备资源利用情况。
    - **交互功能**:
        - 筛选器: 用户可选择不同维度组合进行数据筛选和下钻。
        - 图表联动与数据提示: 同客户分析。
        - 时间范围选择: 同客户分析。
- **B. 报表导出**
    - 触发与交互: 同客户分析模块的报表导出功能，允许导出设备分析相关的图表和数据。

##### 4.2.3.3 数据定义 (分析维度与指标)

- **分析维度**: 见4.2.3.2 A. 数据维度部分。包括时间、设备厂商、设备型号、所属省级平台、接入区域、设备类型、设备状态等。
- **关键指标**: 见4.2.3.2 A. 关键指标与可视化展示部分。包括设备总数、各分类设备数及占比、设备在线率、平均离线时长、故障发生频率、视频流平均利用率、存储资源占用情况等。

##### 4.2.3.4 权限控制

- 功能访问权限: 拥有“设备分析-查看”权限的用户可以访问设备分析看板。
- 数据权限 (可选): 可能限制用户查看特定区域或特定类型设备的分析数据。默认可查看所有设备的分析数据。
- 报表导出权限: 可设为与查看权限相同，或单独控制“设备分析-导出”权限。

#### 4.2.4 业务规则

- 数据来源: 设备分析的数据主要来源于适配中心的（省侧）设备管理模块（设备基础信息、状态信息）、（省侧）通道管理模块、南向协议适配模块的交互日志（用于判断在线、故障等），以及可能的流媒体处理模块（用于分析视频流利用率）。
- 指标计算规则:
    - 设备在线率: (当前在线设备数 / 总接入设备数) * 100%。可按日/周/月计算平均在线率。
    - 平均离线时长: 一段时间内，某设备/某类设备的总离线时长 / 离线次数（或设备数量）。
    - 故障发生频率: 一段时间内，某设备/某类设备的故障申告次数或系统检测到的故障事件次数。
    - 视频流平均利用率: (一段时间内，设备上所有视频流被有效访问或处理的总时长) / (设备总运行时长 * 视频流数量)。计算方式需根据实际采集的数据定义。
- 数据更新频率: 同客户分析，通常每日更新，部分状态类指标可更高频。

#### 4.2.5 异常处理方案

- 同客户分析模块的异常处理方案。

#### 4.2.6 与其他功能的关联和依赖

- **依赖项 (Dependencies)**:
    - （省侧）设备管理模块: 提供设备的基础信息、实时状态、厂商型号等。
    - （省侧）通道管理模块: 提供通道相关信息，辅助分析。
    - 南向接口适配模块/省级平台连接状态监控模块: 提供设备连接状态、心跳、故障等原始数据。
    - （省侧）流媒体处理与转发模块: （可能）提供视频流使用情况数据。
- **被依赖项 (Generated Dependencies)**:
    - 无直接被其他功能模块强依赖，其产出的分析结果主要供运维决策和资源优化。

---

### 4.3 功能模块：业务分析

#### 4.3.1 功能描述与目标

- 解决的问题: 运营和产品团队需要了解通过适配中心承载的各类视频业务的整体使用情况、用户行为偏好、业务性能瓶颈以及增长趋势，以便优化业务流程、提升用户体验和规划未来的业务发展方向。
- 用户价值/目标: 通过对视频业务数据的深入分析，发现业务热点和增长点，识别业务运行风险，为业务运营策略调整、产品功能迭代和市场推广提供数据驱动的决策支持。
- 核心能力概述: 针对通过适配中心承载的各类视频业务（如实时视频点播、录像回放、视频上云、智能分析等），统计各项业务的使用总量、并发峰值、用户访问时段分布、成功率等指标；分析不同业务的增长趋势、用户偏好和热点应用场景，为业务发展和运营策略提供数据支撑。 
    

#### 4.3.2 原型参考

- 主要原型页面: 运营分析原型.html - 业务分析标签页

#### 4.3.3 详细需求

##### 4.3.3.1 功能入口与触发条件

- 入口: 运营门户模块 -> 运营分析 -> 业务分析 [参考原型 运营分析原型.html - 业务分析标签页]
- 触发条件: 用户已登录，并拥有“业务分析”功能的查看权限。

##### 4.3.3.2 交互流程与界面详述

- **A. 业务分析看板** [参考原型 运营分析原型.html - 业务分析标签页]
    - 布局: 顶部为筛选条件区（时间范围、业务类型、客户类型、所属区域四个筛选器），中间为关键指标卡片区（4个指标卡片横向排列），下方为图表区域（2x2网格布局展示4个分析图表）。
    - **数据维度 (可用于筛选和分组统计)**:
        - 时间维度: 日、周、月、季度、年，或自定义时间范围。
        - 业务类型: 视频点播、视频直播、设备管理、用户管理、数据同步。
        - 客户类型: 政府客户、企业客户、个人客户。
        - 所属区域: 华北、华东、华南、华中、西南、西北、东北。
    - **关键指标卡片展示**:
        - 总请求数卡片: 显示总请求数（如2.5M），包含较上月增长百分比（如+15.2%）。
        - 成功率卡片: 显示请求成功率（如99.2%），包含成功请求数量。
        - 峰值并发卡片: 显示峰值并发数（如1256），包含平均并发数。
        - 平均响应时间卡片: 显示平均响应时间（如125ms）。
    - **图表区域展示**:
        - 业务类型分布图: 饼图展示不同业务类型请求量占比。
        - 使用量趋势图: 折线图展示业务使用量随时间变化趋势。
        - 24小时访问分布图: 柱状图展示24小时内访问量分布。
        - 并发分析图: 组合图表展示并发量相关指标。
    - **交互功能**:
        - 筛选器: 用户可选择不同维度组合进行数据筛选和下钻。
        - 图表联动与数据提示: 同客户分析。
        - 时间范围选择: 同客户分析。
- **B. 报表导出**
    - 触发与交互: 同客户分析模块的报表导出功能，允许导出业务分析相关的图表和数据。

##### 4.3.3.3 数据定义 (分析维度与指标)

- **分析维度**: 见4.3.3.2 A. 数据维度部分。包括时间、业务类型、客户维度（ID、行业、级别）、区域/设备维度（可选）等。
- **关键指标**: 见4.3.3.2 A. 关键指标与可视化展示部分。包括业务使用总量（次数、时长、流量）、并发峰值、平均并发、请求成功率、平均响应时延、用户访问时段分布、热门资源/功能等。

##### 4.3.3.4 权限控制

- 功能访问权限: 拥有“业务分析-查看”权限的用户可以访问业务分析看板。
- 数据权限 (可选): 可能限制用户查看特定客户群体或特定业务类型的分析数据。默认可查看所有业务分析数据。
- 报表导出权限: 可设为与查看权限相同，或单独控制“业务分析-导出”权限。

#### 4.3.4 业务规则

- 数据来源: 业务分析的数据主要来源于适配中心处理各类视频业务时产生的业务日志、接口调用日志、流媒体会话日志等。部分分析可能需要关联客户信息管理模块和设备管理模块的数据。
- 指标计算规则:
    - 使用总量: 如视频点播次数、录像回放总时长。
    - 并发峰值: 在统计周期内（如每分钟、每5分钟）同时使用某项业务的最大用户数或会话数。
    - 请求成功率: (成功的业务请求次数 / 总的业务请求次数) * 100%。
    - 用户访问时段分布: 按小时或特定时间段统计业务请求量或活跃用户数。
- 数据更新频率: 同客户分析，通常每日进行ETL和汇总计算。并发等实时性要求高的指标，其统计周期应更短。

#### 4.3.5 异常处理方案

- 同客户分析模块的异常处理方案。

#### 4.3.6 与其他功能的关联和依赖

- **依赖项 (Dependencies)**:
    - 各具体视频业务处理模块（如实时点播服务、录像回放服务、视频上云接口、智能分析引擎接口等）的日志记录功能。
    - 北向接口调用日志。
    - （省侧）流媒体处理与转发模块的会话日志。
- **被依赖项 (Generated Dependencies)**:
    - 无直接被其他功能模块强依赖，其产出的分析结果主要供业务决策、产品优化和运营策略制定。
