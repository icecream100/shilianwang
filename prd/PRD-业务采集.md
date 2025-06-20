# 需求文档 - 业务采集

## 1. 功能概述

- 1.1 功能名称：业据采集
- 1.2 功能概述：本模块负责配置、执行并监控从各类外部数据源（包括已对接的省级视频业务平台、省侧CRM系统）的数据采集任务，以及适配中心自身运行状态数据的收集。其核心目标是确保准确、及时地获取运营分析、业务监控及平台运维所需的各类原始数据，并为这些数据的采集过程提供灵活的配置管理和状态展现能力。

## 2. 用户与场景

- 2.1 目标用户: 省级适配中心系统管理员、运维工程师、数据分析配置人员。
- 2.2 用户场景/故事:
    - 场景一：作为一个省级适配中心系统管理员，我希望能配置从各个已接入的省级视频平台（如千里眼）定期采集其设备元数据、用户访问行为以及视频业务统计数据，以便为后续的运营分析提供数据基础。
    - 场景二：作为一个省级适配中心数据对接负责人，我需要配置与省侧CRM系统的接口参数、字段映射和同步频率，以确保客户信息能够准确、自动地同步到适配中心，支持客户管理和客户分析功能。
    - 场景三：作为一个省级适配中心运维工程师，我需要一个集中的界面来实时查看数据同步任务的执行情况，以便快速发现和定位潜在的运行问题。
    - 场景四：作为一个省级适配中心系统管理员，当某个省级视频平台的数据接口发生变更或新增了可采集的数据类型时，我希望能方便地修改对应的数据采集任务配置，以适应这些变化。

## 3. 功能范围/列表

- 3.1 功能模块一: 业务采集设置
- 3.2 功能模块二: 客户同步设置
- 3.3 功能模块三: 任务状态

## 4. 功能模块详情

---

### 4.1 功能模块：业务采集设置

#### 4.1.1 功能描述与目标

- 解决问题: 需要一个配置界面来管理从已对接的各省级视频平台（如千里眼、移动看家）采集特定业务数据的任务，明确采集内容、频率和方式。
- 用户价值/目标: 实现对省级视频平台各类运行数据的按需、可配置化采集，确保数据采集的全面性和准确性，为上层数据应用提供原始数据支撑。
- 核心能力概述: 通过南向接口适配模块，主动从已对接的省级视频平台（如千里眼、移动看家）定期或实时采集各类数据 1。包括：设备和通道的详细元数据（如型号、固件版本、安装位置、能力集等）；用户通过这些平台的访问行为数据（如登录次数、视频查看时长）；视频业务数据（如录像存储时长、智能分析事件触发次数）；以及平台自身的业务办理数据（如套餐订购信息，需平台开放接口） 2。本功能提供对这些采集任务的配置管理。
    

#### 4.1.2 原型参考

- 主要原型页面: 业务采集原型.html - 业务采集设置页面（包含配置列表、新增/编辑配置对话框、配置详情弹窗）

#### 4.1.3 详细需求

##### 4.1.3.1 功能入口与触发条件

- 入口: 侧边栏导航 -> 业务数据采集 -> 业务采集设置 [参考原型 业务采集原型.html]
- 触发条件: 用户已登录，并拥有"业务采集设置"权限。

##### 4.1.3.2 交互流程与界面详述

- **A. 数据采集任务列表与筛选**: [参考原型 业务采集原型.html - 业务采集设置]
    - 布局: 顶部为筛选区域和"新增采集配置"按钮，下方为已配置的数据采集任务列表，底部为分页控件。
    - 包含元素:
        - 筛选器: 支持按配置名称（搜索框）、平台名称（下拉选择）、源平台（下拉选择）、数据类型（下拉选择）、状态（下拉选择）进行筛选，包含搜索按钮。
        - "新增采集配置"按钮（蓝色主按钮）。
        - 列表: 表格形式展示，包含复选框列用于批量操作。关键列包括：配置名称、源平台、采集数据类型、采集方式、采集频率、启用状态（开关控件）、最后执行时间、执行状态（带颜色标签）。操作列包含：详情、编辑、手动触发、删除按钮。
        - 分页控件: 显示总条数，支持页码跳转和每页条数设置。
    - 默认交互/排序: 列表默认按创建时间降序，支持表头排序。
- **B. 新增/编辑业务采集设置**: [参考原型 业务采集原型.html - 新增/编辑业务数据采集配置对话框]
    - 触发: 点击"新增采集配置"按钮或已有配置的"编辑"按钮。
    - 交互步骤:
        - Step 1: 系统弹出"新增业务数据采集配置"或"编辑业务数据采集配置"对话框（模态窗口）。
        - Step 2: 用户输入配置名称（必填文本框）。
        - Step 3: 选择源平台（下拉选择，选项包括：千里眼平台、移动看家、GB/T 28181）。
        - Step 4: 选择需要采集的数据类型（多选复选框组）：
            - 设备/通道元数据：设备基本信息、通道配置等
            - 用户行为数据：登录记录、操作日志等
            - 视频业务数据：点播统计、直播数据等
            - 套餐信息：用户套餐、计费信息等
        - Step 5: 配置采集方式（单选按钮组）：
            - 周期性拉取：定时从源平台获取数据
            - 实时订阅：接收平台推送的实时数据
        - Step 6: 配置采集频率（下拉选择或自定义）：
            - 预设选项：每小时、每日、每周、每月
            - 自定义CRON表达式输入框
        - Step 7: 输入采集参数（可选文本域）：用于配置特定的API参数或过滤条件。
        - Step 8: 设置启用状态（开关控件，默认开启）。
        - Step 9: 用户点击"确定"保存或"取消"关闭。
        - Step 10: 前后端校验：配置名称唯一性、必填字段完整性、CRON表达式有效性等。
        - Step 11: 成功则保存配置，关闭对话框，刷新列表，显示成功提示；失败则在对话框内显示错误信息。
- **C. 查看采集任务详情与状态**: [参考原型 业务采集原型.html - 配置详情弹窗]
    - 触发: 点击配置列表中的"详情"按钮。
    - 交互: 弹出"配置详情"对话框，以只读形式展示：
        - 基本信息：配置名称、数据源类型、采集频率、启用状态
        - 执行信息：最后执行时间、下次执行时间、API地址
        - 配置参数：采集参数的详细内容
        - 描述信息：配置的详细说明
        - 操作按钮：关闭按钮
- **D. 启用/停用采集任务**:
    - 触发: 点击配置列表中的"启用"或"停用"按钮。
    - 交互: 二次确认后，更新任务的启用状态。停用后，对应的采集活动将暂停。
- **E. 手动触发一次采集**:
    - 触发: 点击配置列表中的"手动触发一次"按钮。
    - 交互: 二次确认后，后台立即执行一次该配置定义的采集任务，并记录执行日志。

##### 4.1.3.3 字段定义与数据规则 (配置项)

|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
|**字段名称**|**字段标识 (Eng)**|**数据类型 & 长度**|**界面显隐/读写**|**约束/规则**|**数据来源/去向**|**备注/说明**|
|配置ID|configId|Long|隐藏/只读|系统生成|系统生成|主键|
|配置名称|configName|String(100)|显示/读写|必填，唯一|用户输入||
|源省级平台内码|sourcePlatformInternalId|Long|隐藏/关联|必填|用户从接入平台列表选择||
|源省级平台名称|sourcePlatformName|String(100)|显示/只读||关联显示||
|采集数据类型|dataTypesToCollect|List&lt;String>|显示/多选|必填，至少选一项。选项基于平台能力预定义。|用户选择|如：DEVICE_METADATA, CHANNEL_METADATA, USER_ACCESS_LOGS, VIDEO_STATS|
|采集参数|collectionParams|JSON/Text|显示/读写（高级）|可选，针对特定数据类型的细化参数|用户输入||
|采集方式|collectionMode|Enum(PERIODIC_PULL, REALTIME_SUBSCRIBE)|显示/选择|必填|用户选择||
|采集频率 (CRON)|collectionFrequencyCron|String(50)|若方式为PULL则显示/读写|条件性必填|用户输入/选择预设||
|启用状态|enabledStatus|Boolean|显示/读写|默认为true|用户选择||

##### 4.1.3.4 权限控制

- 查看/编辑/删除/启停用业务采集设置: 需要特定权限，如“业务采集设置管理”。
- 手动触发采集: 通常与编辑权限一致。

#### 4.1.4 业务规则

- 一个源省级平台可以有多个数据采集配置，分别针对不同类型的数据或不同频率。
- 采集的数据项和能力高度依赖于具体省级视频平台的接口开放程度和协议规范。配置界面应尽可能清晰地反映这些依赖。
- 采集到的原始数据应进行初步的格式化和校验，并存储到适配中心的原始数据层或数据湖中，供后续处理和分析。
- 采集任务的执行状态和结果（成功/失败、采集数据量等）需要被详细记录。

#### 4.1.5 异常处理方案

- 源平台接口不可达或认证失败: 采集任务执行时，若无法连接源平台或认证失败，应记录错误，标记任务执行失败，并可配置告警通知。
- 请求的数据类型平台不支持或无数据: 记录正常，但采集数据量为零或有特定提示。
- 数据解析或格式转换失败: 记录错误，尽可能不中断整个采集批次，标记问题数据。

#### 4.1.6 与其他功能的关联和依赖

- **依赖项 (Dependencies)**:
    - 接入平台管理模块: 采集配置必须选择一个已成功配置并启用的省级视频平台。
    - 南向接口适配模块: 实际执行数据采集的动作依赖此模块的协议交互能力。
- **被依赖项 (Generated Dependencies)**:
    - 运营分析模块: 采集到的运行业务数据是进行设备分析、业务分析等的重要数据源。
    - 驾驶舱模块: 部分运营指标可能来源于此采集的数据。
    - （本模块下）任务状态: 可能展示这些采集任务的执行状态。

---

### 4.2 功能模块：客户同步设置

#### 4.2.1 功能描述与目标

- 解决问题: 需要一个标准化的方式来配置和管理与省侧CRM系统的数据对接，实现客户信息的自动同步，包括处理字段差异和数据格式转换。
- 用户价值/目标: 确保适配中心能够及时、准确地获取最新的客户基础信息，减少人工录入和信息不一致的风险，为客户管理、客户授权以及客户相关的运营分析提供可靠的数据基础。
- 核心能力概述: 提供专门的接口配置和管理功能，用于设定与省侧CRM（客户关系管理）系统的对接参数 3。包括CRM系统的API地址、认证方式、数据查询条件、同步频率（如每日一次）等 4。核心是支持客户数据字段的自定义映射规则和简单的数据转换逻辑（如代码值转换），确保CRM中的客户信息能准确同步至适配中心 5。
    

#### 4.2.2 原型参考

- 主要原型页面: 业务采集原型.html - 客户同步设置页面（包含CRM配置、字段映射配置、同步日志查看）

#### 4.2.3 详细需求

##### 4.2.3.1 功能入口与触发条件

- 入口: 侧边栏导航 -> 业务数据采集 -> 客户同步设置 [参考原型 业务采集原型.html]
- 触发条件: 用户已登录，并拥有"客户同步设置"权限。

##### 4.2.3.2 交互流程与界面详述

- **A. CRM系统配置**: [参考原型 业务采集原型.html - 客户同步设置]
    - 布局: 顶部为CRM系统基本配置区域，包含API配置、认证设置、同步频率等。
    - 包含元素:
        - API地址配置（文本输入框）：输入CRM系统的API接口地址
        - 认证类型选择（下拉选择）：支持API Key、OAuth 2.0、Basic Auth等认证方式
        - 认证参数配置（根据认证类型动态显示相应输入框）
        - 同步频率设置（下拉选择）：每小时、每日、每周、自定义CRON表达式
        - 启用状态开关
        - "测试连接"按钮：验证CRM系统连接是否正常
        - "保存配置"按钮：保存CRM系统配置
    - 交互流程:
        - Step 1: 用户输入CRM系统API地址。
        - Step 2: 选择认证类型，系统根据选择动态显示对应的认证参数输入框。
        - Step 3: 输入认证参数（如API Key、用户名密码等）。
        - Step 4: 设置同步频率和启用状态。
        - Step 5: 点击"测试连接"验证配置是否正确。
        - Step 6: 测试成功后，点击"保存配置"保存设置。
- **B. 字段映射配置**: [参考原型 业务采集原型.html - 字段映射配置]
    - 布局: 中部为字段映射配置区域，左侧显示本地字段，右侧显示CRM字段，中间为映射关系配置。
    - 包含元素:
        - 本地字段列表：显示适配中心客户信息的标准字段（如客户ID、客户名称、联系电话、地址等）
        - CRM字段列表：显示从CRM系统获取的可用字段列表
        - 映射关系配置：通过下拉选择或拖拽方式建立本地字段与CRM字段的对应关系
        - 数据转换规则：为特定字段配置数据格式转换规则（如日期格式、代码值映射等）
        - "刷新CRM字段"按钮：重新获取CRM系统的字段列表
        - "保存映射"按钮：保存字段映射配置
    - 交互流程:
        - Step 1: 系统自动加载本地客户字段和CRM系统字段。
        - Step 2: 用户为每个本地字段选择对应的CRM字段。
        - Step 3: 为需要转换的字段配置转换规则。
        - Step 4: 点击"保存映射"保存配置。
- **C. 同步任务管理**: [参考原型 业务采集原型.html - 同步任务管理]
    - 布局: 包含手动触发同步、查看同步状态、同步历史记录等功能。
    - 包含元素:
        - "立即同步"按钮：手动触发一次客户数据同步
        - 同步状态显示：当前同步任务的执行状态（运行中、已完成、失败等）
        - 同步进度条：显示当前同步任务的进度
        - 最近同步记录：显示最近几次同步的基本信息（时间、状态、同步数量等）
    - 交互流程:
        - Step 1: 用户点击"立即同步"按钮。
        - Step 2: 系统启动同步任务，显示进度条和状态信息。
        - Step 3: 同步完成后，更新同步记录和状态显示。
- **D. 同步日志查看**: [参考原型 业务采集原型.html - 同步日志弹窗]
    - 触发: 点击"查看同步日志"按钮或同步记录的详情链接。
    - 交互: 弹出"同步日志"对话框，显示详细的同步执行信息：
        - 同步时间：任务开始和结束时间
        - 同步状态：成功、失败、部分成功
        - 数据统计：总数量、成功数量、失败数量、跳过数量
        - 执行耗时：任务总耗时
        - 错误信息：如果有失败记录，显示具体的错误原因
        - 操作按钮：关闭、导出日志

##### 4.1.3.3 字段定义与数据规则 (配置项)

|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
|**字段名称**|**字段标识 (Eng)**|**数据类型 & 长度**|**界面显隐/读写**|**约束/规则**|**数据来源/去向**|**备注/说明**|
|CRM API地址|crmApiUrl|String(255)|显示/读写|必填，有效URL|管理员输入||
|CRM认证方式|crmAuthType|Enum|显示/选择|必填|管理员选择||
|CRM认证参数|crmAuthParams|JSON/Text|显示/读写|条件性必填|管理员输入||
|CRM数据查询条件|crmQueryFilter|String(500)|显示/读写|可选|管理员输入||
|CRM同步频率(CRON)|crmSyncFrequencyCron|String(50)|显示/读写|必填|管理员输入/选择预设||
|CRM字段映射规则|crmFieldMappingRules|JSON/Text|通过专用界面配置/内部存储|必填|管理员配置||
|CRM同步启用状态|crmSyncEnabled|Boolean|显示/读写|默认为true|管理员选择||

##### 4.1.3.4 权限控制

- 查看/编辑客户同步设置、字段映射、手动触发同步、查看日志: 需要特定权限，如“CRM数据同步配置管理”。

#### 4.2.4 业务规则

- 同步来的CRM客户信息将作为适配中心内客户数据的主要来源或重要补充，用于客户管理、授权、分析等。
- 字段映射和转换规则的正确性对数据质量至关重要。应提供预览或测试功能（可选）。
- 同步冲突处理：若适配中心内已有手动创建的客户与CRM同步来的客户可识别为同一实体，需有明确的冲突解决策略（如CRM优先、提示人工合并等，此策略在客户管理模块中定义，此处配置保证同步）。
- 同步任务的健壮性：应能处理网络波动、CRM接口临时不可用等情况，支持重试机制。

#### 4.2.5 异常处理方案

- CRM接口连接/认证失败: 在“测试连接”或实际同步时，明确提示错误信息，记录日志，不更新数据。
- 字段映射配置错误或数据转换失败: 记录详细错误日志，标记受影响的客户数据，尽可能不中断整个同步批次。
- 同步过程中部分数据校验失败: 按条记录失败原因，整体任务可标记为“部分成功”。

#### 4.2.6 与其他功能的关联和依赖

- **依赖项 (Dependencies)**:
    - 省侧CRM系统的API接口。
    - 适配中心客户信息的数据模型定义 (客户管理模块)。
- **被依赖项 (Generated Dependencies)**:
    - 客户信息管理模块: 同步的客户数据会写入此模块管理的数据表。
    - 运营分析模块 (客户分析): 以同步的CRM数据为重要分析数据源。
    - （本模块下）任务状态: 可能展示CRM同步任务的执行状态。

---

### 4.3 功能模块：任务状态

#### 4.3.1 功能描述与目标

- 解决问题: 运维人员需要一个集中的视图来监控适配中心自身各服务模块的健康状况、与各省级视频平台的连接交互状态，以及数据同步任务的整体情况，以便及时发现系统瓶颈或故障。
- 用户价值/目标: 提供对适配中心底层运行状态和数据采集通道健康度的透明化监控，保障数据采集的稳定性和可靠性，支持平台的整体稳定运行。
- 核心能力概述: 持续监控采集与这些平台接口调用的成功率、失败率、平均响应时间、数据同步任务的执行状态、成功同步的数据量及同步延迟等关键交互状态数据 9。
    

#### 4.3.2 原型参考

- 主要原型页面: 业务采集原型.html - 任务状态页面（包含系统健康监控、平台连接状态、任务执行记录）

#### 4.3.3 详细需求

##### 4.3.3.1 功能入口与触发条件

- 入口: 侧边栏导航 -> 业务数据采集 -> 任务状态 [参考原型 业务采集原型.html]
- 触发条件: 用户已登录，并拥有"任务状态查看"权限。

##### 4.3.3.2 交互流程与界面详述

- **A. 系统健康监控仪表板**: [参考原型 业务采集原型.html - 任务状态]
    - 布局: 顶部为系统健康状态概览卡片，包含CPU、内存、磁盘、网络等关键指标。
    - 包含元素:
        - 系统资源监控卡片:
            - CPU使用率：显示当前CPU使用百分比，带有状态颜色指示（绿色正常、黄色警告、红色异常）
            - 内存使用率：显示内存使用情况和可用内存
            - 磁盘使用率：显示磁盘空间使用情况
            - 网络状态：显示网络连接状态和流量情况
        - 微服务状态监控:
            - 各微服务模块的运行状态（运行中、停止、异常）
            - 服务响应时间和健康检查结果
            - 服务重启次数和最后重启时间
        - 自动刷新控制：支持设置自动刷新间隔（30秒、1分钟、5分钟）
    - 交互: 实时显示系统健康状态，支持点击查看详细信息。
- **B. 平台连接状态监控**: [参考原型 业务采集原型.html - 平台连接状态]
    - 布局: 中部为已配置平台的连接状态列表，显示各平台的连接健康度。
    - 包含元素:
        - 平台连接状态列表:
            - 平台名称：显示已配置的各个省级视频平台名称
            - 连接状态：在线、离线、连接异常（带颜色标识）
            - 最后连接时间：显示最近一次成功连接的时间
            - 响应时间：显示平台API的平均响应时间
            - 错误次数：显示最近24小时内的连接错误次数
        - 操作按钮:
            - "测试连接"：手动测试特定平台的连接状态
            - "查看详情"：查看平台连接的详细信息和历史记录
            - "刷新状态"：刷新所有平台的连接状态
    - 交互流程:
        - Step 1: 系统定期检测各平台连接状态并更新显示。
        - Step 2: 用户可点击"测试连接"手动验证特定平台。
        - Step 3: 点击"查看详情"可查看平台连接的详细信息。
- **C. 任务执行记录**: [参考原型 业务采集原型.html - 任务记录]
    - 布局: 底部为任务执行记录列表，显示所有数据采集和同步任务的执行情况。
    - 包含元素:
        - 任务记录筛选器:
            - 任务名称搜索框
            - 任务类型筛选（业务数据采集、客户同步、全部）
            - 执行状态筛选（成功、失败、运行中、全部）
            - 时间范围选择器
        - 任务记录列表:
            - 任务名称：显示具体的任务配置名称
            - 任务类型：业务数据采集、客户同步等
            - 执行时间：任务开始执行的时间
            - 执行耗时：任务执行的总时长
            - 执行状态：成功、失败、运行中（带颜色标签）
            - 处理数量：成功处理的数据条数
            - 错误信息：如果执行失败，显示简要错误信息
        - 操作列:
            - "查看详情"：查看任务执行的详细日志
            - "重试"：对失败的任务进行重试（仅失败任务显示）
        - 分页控件：支持分页浏览和每页条数设置
    - 交互流程:
        - Step 1: 用户可通过筛选器快速定位特定类型或状态的任务。
        - Step 2: 点击"查看详情"查看任务的详细执行日志。
        - Step 3: 对于失败的任务，可点击"重试"重新执行。
- **D. 任务详情查看**: [参考原型 业务采集原型.html - 任务详情弹窗]
    - 触发: 点击任务记录列表中的"查看详情"按钮。
    - 交互: 弹出"任务详情"对话框，显示任务执行的完整信息：
        - 基本信息：任务名称、类型、执行时间、耗时、状态
        - 执行参数：任务执行时使用的配置参数
        - 执行结果：处理的数据量、成功数量、失败数量
        - 错误日志：详细的错误信息和堆栈跟踪（如有）
        - 操作按钮：关闭、导出日志、重试（失败任务）

##### 4.1.3.3 数据定义 (展示的指标与状态)

数据同步任务执行状态(成功/失败/进行中)、成功同步数据量(条/MB)、数据同步延迟(秒/分钟)。

##### 4.1.3.4 权限控制

- 查看任务状态页面: 需要特定权限，如“采集与系统状态监控”。

#### 4.3.4 业务规则

- 展示的数据应尽可能实时或准实时，以反映当前系统的真实运行状况。
- 本模块主要用于状态展示和快速诊断，详细的日志查询和故障排除可能需要跳转到其他更专业的日志或运维管理模块。
- 指标的正常/警告/危险阈值应可配置（后台配置或系统预设）。

#### 4.3.5 异常处理方案

- 数据获取失败或延迟: 若无法从后端获取最新的状态数据，界面应显示“数据加载中...”或“数据获取失败，请刷新”等提示。
- 部分指标不可用: 若某些指标因依赖的服务未启动或配置问题而无法采集，应在该指标的展示区域明确提示“指标不可用”或“数据源配置错误”。

#### 4.3.6 与其他功能的关联和依赖

- **依赖项 (Dependencies)**:
    - 省级平台连接与交互状态的探测和日志记录组件。
    - （本PRD定义的）业务采集设置模块和客户同步设置模块: 获取这些采集任务的配置信息和执行状态。
    - 接入平台管理模块: 获取已配置的省级平台列表信息。
- **被依赖项 (Generated Dependencies)**:
    - （间接）运维人员和系统管理员: 依赖此模块提供的信息进行日常监控和故障初步判断。
    - （可能）告警管理模块: 本模块监控到的异常状态可能会触发告警。