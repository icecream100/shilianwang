# 需求文档 - 日志管理

## 1. 功能概述

- 1.1 功能名称：日志管理
- 1.2 功能概述：日志管理模块为视联网省级适配中心提供全面的日志记录、查询和展示功能。它负责收集并存储适配中心运行过程中的各类关键日志，包括用户登录行为、用户在门户内的重要操作等。

## 2. 用户与场景

- 2.1 目标用户: 省级适配中心系统管理员、运维工程师、安全审计员、技术支持人员。
- 2.2 用户场景/故事:
    - 场景一：作为一个省级适配中心运维工程师，当用户报告无法登录时，我希望能快速查询该用户的登录日志，查看其尝试登录的时间、IP地址及登录结果，以便定位问题原因。
    - 场景二：作为一个省级适配中心系统管理员，当需要审计某项配置（如资源授权）是如何被修改的时，我希望能查询操作日志，追溯到具体的操作人、操作时间以及修改的内容详情。

## 3. 功能范围/列表

- 3.1 功能模块一: 登录日志
- 3.2 功能模块二: 操作日志

## 4. 功能模块详情

---

### 4.1 功能模块：登录日志

#### 4.1.1 功能描述与目标

- 解决问题: 需要记录所有用户尝试登录适配中心门户的行为，包括成功和失败的尝试，以便进行安全审计和问题排查。
- 用户价值/目标: 提供用户登录行为的可追溯性，帮助管理员监控异常登录尝试，保障系统账户安全，并为用户登录问题提供诊断依据。
- 核心能力概述: 自动记录用户登录适配中心门户的详细信息，包括登录用户、登录时间、来源IP、登录结果（成功/失败）及失败原因。提供按条件查询和展示登录日志的功能。

#### 4.1.2 原型参考

- 主要原型页面: [日志管理原型.html](../html_prototypes/日志管理原型.html) - 登录日志页面

#### 4.1.3 详细需求

##### 4.1.3.1 功能入口与触发条件

- 入口: 左侧导航菜单 -> 运营门户 -> 日志管理 -> 登录日志 [参考原型 日志管理原型.html]
- 触发条件: 用户已登录，并拥有"登录日志查看"权限。

##### 4.1.3.2 交互流程与界面详述

- 主界面/列表描述: [参考原型 日志管理原型.html - 登录日志页面]
    - 布局: 顶部为页面标题和描述区域，中间为筛选条件区域，下方为登录日志列表表格，底部为分页组件
    - 包含元素: 
        - 页面标题："登录日志"
        - 页面描述："查看和管理用户登录行为记录，包括成功和失败的登录尝试"
        - 筛选条件区域：用户名输入框、登录IP地址输入框、登录结果下拉选择、登录时间范围选择器
        - 操作按钮：查询按钮、重置按钮
        - 登录日志列表表格：显示日志ID、用户名、登录IP地址、登录地理位置、客户端类型、登录时间、登录状态、失败原因、操作列
    - 默认交互/排序: 列表默认按登录时间降序排列，支持分页显示

- 核心操作流程细化:
    - A. 查询登录日志 流程:
        - 触发: 用户在筛选条件区域输入查询条件，点击"查询"按钮
        - 交互步骤:
            - Step 1: 用户在筛选条件区域输入查询条件（用户名、登录IP、登录结果、时间范围）
            - Step 2: 用户点击"查询"按钮
            - Step 3: 系统显示加载状态，表格显示loading效果
            - Step 4: 后端根据查询条件检索登录日志数据
            - Step 5: 结果处理:
                - 成功: 表格刷新显示符合条件的登录日志列表，更新分页信息，显示"查询完成"提示
                - 失败: 显示错误提示信息，保持原有数据显示
            - Step 6: 用户可点击"重置"按钮清空所有筛选条件
    
    - B. 查看登录日志详情 流程:
        - 触发: 用户点击登录日志列表中某条记录的"详情"按钮
        - 交互步骤:
            - Step 1: 用户点击日志记录操作列的"详情"按钮
            - Step 2: 系统弹出"登录日志详情"对话框 [参考原型 日志管理原型.html - 登录日志详情对话框]
            - Step 3: 对话框显示该条登录日志的完整信息，包括：日志ID、用户名、登录IP、登录地理位置、客户端类型、登录时间、登录状态、失败原因、会话ID等
            - Step 4: 用户可点击"关闭"按钮或对话框外部区域关闭详情对话框

##### 4.1.3.3 字段定义与数据规则

| 字段名称 | 字段标识 (Eng) | 数据类型 & 长度 | 界面显隐/读写 | 约束/规则 | 数据来源/去向 | 备注/说明 |
|----------|----------------|-----------------|---------------|-----------|---------------|----------|
| 日志ID | logId | Long | 列表显示/只读 | 系统生成，唯一 | 系统生成 | 主键 |
| 用户名 | username | String(50) | 列表显示/只读 | 必填，记录尝试登录的用户名 | 登录请求 | |
| 登录IP地址 | loginIp | String(45) | 列表显示/只读 | 必填，IPv4或IPv6格式 | 请求来源 | |
| 登录地理位置 | loginLocation | String(100) | 列表显示/只读 | 可为空，根据IP解析 | IP地址解析服务 | |
| 客户端类型 | clientType | String(100) | 列表显示/只读 | 可为空，解析User-Agent | 请求头信息 | 如：Chrome浏览器、移动端等 |
| 登录时间 | loginTime | DateTime | 列表显示/只读 | 必填，精确到秒 | 系统时间 | 格式：YYYY-MM-DD HH:mm:ss |
| 登录状态 | loginStatus | Enum | 列表显示/只读 | 必填，SUCCESS/FAILURE | 认证结果 | 成功显示绿色标签，失败显示红色标签 |
| 失败原因 | failureReason | String(255) | 列表显示/只读 | 登录失败时必填 | 认证模块 | 如：密码错误、用户不存在等 |
| 会话ID | sessionId | String(100) | 详情显示/只读 | 成功登录时生成 | 会话管理 | 用于关联用户会话 |

##### 4.1.3.4 权限控制

- 功能访问权限: 拥有"登录日志查看"权限的用户可以访问并查询登录日志
- 操作权限: 查看登录日志列表和详情需要"登录日志查看"权限
- 数据权限: 系统管理员可查看所有用户的登录日志；普通管理员根据权限配置可能只能查看特定范围的日志

#### 4.1.4 业务规则

- 核心算法或逻辑说明:
    - 登录日志自动记录: 所有用户（包括管理员和普通用户）尝试登录适配中心门户的行为均需被自动记录
    - 实时性要求: 日志应近实时生成并可供查询，延迟不超过5秒
    - 地理位置解析: 系统应尝试根据IP地址解析登录地理位置，解析失败时该字段为空
    - 客户端信息提取: 从User-Agent中提取并解析客户端类型信息
- 限制条件与边界情况:
    - 限制条件:
        - 查询时间范围限制：单次查询时间跨度不超过90天
        - 查询结果数量限制：单次查询返回结果不超过10000条
        - 本地日志保留期限：适配中心本地保留近90天的登录日志
    - 边界情况处理:
        - 列表为空：显示"暂无登录日志数据"的提示
        - 查询无结果：显示"未找到符合条件的登录日志"
        - IP地址解析失败：登录地理位置字段显示为空或"未知"
        - 超大数据量查询：提示用户缩小查询范围，避免系统性能影响

#### 4.1.5 异常处理方案

- 查询超时或失败: 若查询日志数据量过大或数据库响应慢，应有30秒超时控制，超时后提示"查询超时，请缩小查询范围后重试"
- 网络异常: 查询请求失败时提示"网络连接失败，请检查网络后重试"
- 服务器内部错误: 显示通用错误提示"系统繁忙，请稍后重试"
- 无符合条件的日志: 列表为空时，显示"未找到符合条件的登录日志"

#### 4.1.6 与其他功能的关联和依赖

- 依赖项 (Dependencies):
    - 用户认证模块: 登录行为由认证模块处理，并触发日志记录
    - 权限管理模块: 依赖权限配置控制日志查看访问
- 被依赖项 (Generated Dependencies):
    - 安全审计流程: 登录日志是安全审计的重要输入
    - 运维排障: 用于诊断用户登录问题

---

### 4.2 功能模块：操作日志

#### 4.2.1 功能描述与目标

- 解决问题: 需要追踪和记录用户在适配中心门户内执行的各项关键操作，以便进行行为审计、责任认定和问题追溯。
- 用户价值/目标: 提供用户操作行为的透明度和可审计性，加强系统安全性，帮助管理员监控敏感操作，并在发生配置错误或违规操作时提供追查依据。
- 核心能力概述: 详细记录用户在适配中心门户执行的关键操作，如配置修改（例如：接入平台配置、设备补充信息编辑、CRM同步配置、角色权限分配等）、资源授权、手动数据同步触发等。提供按条件查询和展示操作日志的功能。

#### 4.2.2 原型参考

- 主要原型页面: [日志管理原型.html](../html_prototypes/日志管理原型.html) - 操作日志页面

#### 4.2.3 详细需求

##### 4.2.3.1 功能入口与触发条件

- 入口: 左侧导航菜单 -> 运营门户 -> 日志管理 -> 操作日志 [参考原型 日志管理原型.html]
- 触发条件: 用户已登录，并拥有"操作日志查看"权限。

##### 4.2.3.2 交互流程与界面详述

- 主界面/列表描述: [参考原型 日志管理原型.html - 操作日志页面]
    - 布局: 顶部为页面标题和描述区域，中间为筛选条件区域，下方为操作日志列表表格，底部为分页组件
    - 包含元素:
        - 页面标题："操作日志"
        - 页面描述："查看和管理用户在系统中执行的关键操作记录"
        - 筛选条件区域：操作用户输入框、操作模块下拉选择、操作类型下拉选择、操作对象输入框、操作结果下拉选择、操作时间范围选择器
        - 操作按钮：查询按钮、重置按钮
        - 操作日志列表表格：显示日志ID、操作用户、用户IP、模块名称、功能名称、操作类型、目标对象描述、操作时间、操作结果、结果消息、操作列
    - 默认交互/排序: 列表默认按操作时间降序排列，支持分页显示

- 核心操作流程细化:
    - A. 查询操作日志 流程:
        - 触发: 用户在筛选条件区域输入查询条件，点击"查询"按钮
        - 交互步骤:
            - Step 1: 用户在筛选条件区域输入查询条件（操作用户、操作模块、操作类型、操作对象、操作结果、时间范围）
            - Step 2: 用户点击"查询"按钮
            - Step 3: 系统显示加载状态，表格显示loading效果
            - Step 4: 后端根据查询条件检索操作日志数据
            - Step 5: 结果处理:
                - 成功: 表格刷新显示符合条件的操作日志列表，更新分页信息，显示"查询完成"提示
                - 失败: 显示错误提示信息，保持原有数据显示
            - Step 6: 用户可点击"重置"按钮清空所有筛选条件
    
    - B. 查看操作日志详情 流程:
        - 触发: 用户点击操作日志列表中某条记录的"详情"按钮
        - 交互步骤:
            - Step 1: 用户点击日志记录操作列的"详情"按钮
            - Step 2: 系统弹出"操作日志详情"对话框 [参考原型 日志管理原型.html - 操作日志详情对话框]
            - Step 3: 对话框显示该条操作日志的完整信息，包括：日志ID、操作用户、用户IP、模块名称、功能名称、操作类型、目标对象类型、目标对象ID、目标对象描述、操作时间、操作状态、结果消息、请求载荷、数据变更对比（修改前后）等
            - Step 4: 用户可点击"关闭"按钮或对话框外部区域关闭详情对话框

##### 4.2.3.3 字段定义与数据规则

| 字段名称 | 字段标识 (Eng) | 数据类型 & 长度 | 界面显隐/读写 | 约束/规则 | 数据来源/去向 | 备注/说明 |
|----------|----------------|-----------------|---------------|-----------|---------------|----------|
| 日志ID | logId | Long | 列表显示/只读 | 系统生成，唯一 | 系统生成 | 主键 |
| 操作用户 | username | String(50) | 列表显示/只读 | 必填，执行操作的用户名 | 当前登录用户 | |
| 用户IP | userIp | String(45) | 列表显示/只读 | 必填，操作时用户的IP地址 | 请求来源 | |
| 模块名称 | moduleName | String(100) | 列表显示/只读 | 必填，被操作的功能模块 | 系统定义 | 如：客户管理、设备管理等 |
| 功能名称 | functionName | String(100) | 列表显示/只读 | 必填，具体的功能点 | 系统定义 | 如：新增客户、修改设备等 |
| 操作类型 | operationType | Enum | 列表显示/只读 | 必填，操作的具体类型 | 系统定义 | CREATE/UPDATE/DELETE/ENABLE/DISABLE/AUTHORIZE/EXPORT等 |
| 目标对象类型 | targetObjectType | String(50) | 详情显示/只读 | 可为空，被操作对象的类型 | 业务逻辑 | 如：Customer、Device、Platform等 |
| 目标对象ID | targetObjectId | String(100) | 详情显示/只读 | 可为空，被操作对象的ID | 业务数据 | |
| 目标对象描述 | targetObjectDesc | String(255) | 列表显示/只读 | 可为空，被操作对象的描述 | 业务数据 | 如：客户名称、设备名称等 |
| 操作时间 | operationTime | DateTime | 列表显示/只读 | 必填，精确到秒 | 系统时间 | 格式：YYYY-MM-DD HH:mm:ss |
| 操作结果 | operationStatus | Enum | 列表显示/只读 | 必填，SUCCESS/FAILURE | 操作执行结果 | 成功显示绿色标签，失败显示红色标签 |
| 结果消息 | resultMessage | String(500) | 列表显示/只读 | 可为空，操作结果描述 | 业务逻辑 | 成功或失败的具体信息 |
| 请求载荷 | requestPayload | Text | 详情显示/只读 | 可为空，操作的请求参数 | 请求数据 | JSON格式，敏感信息已脱敏 |
| 修改前数据 | dataBefore | Text | 详情显示/只读 | 可为空，修改前的数据快照 | 业务数据 | JSON格式，仅修改操作有值 |
| 修改后数据 | dataAfter | Text | 详情显示/只读 | 可为空，修改后的数据快照 | 业务数据 | JSON格式，仅修改操作有值 |

##### 4.2.3.4 权限控制

- 功能访问权限: 拥有"操作日志查看"权限的用户可以访问并查询操作日志
- 操作权限: 查看操作日志列表和详情需要"操作日志查看"权限
- 数据权限: 系统管理员可查看所有用户的操作日志；普通管理员根据权限配置可能只能查看特定模块或特定用户的操作日志

#### 4.2.4 业务规则

- 核心算法或逻辑说明:
    - 关键操作自动记录: 系统中所有定义为"关键操作"的用户行为均需被自动记录，包括但不限于：客户管理、设备管理、接入平台管理、角色权限、系统配置等模块的增删改操作
    - 数据变更记录: 对于修改类操作，系统应记录修改前后的数据对比，便于审计和回溯
    - 敏感信息脱敏: 请求参数和数据快照在存入日志前，应进行必要的敏感信息脱敏处理（如密码、密钥等字段不应明文记录）
    - 实时性要求: 操作日志应在操作完成后立即记录，延迟不超过3秒
- 限制条件与边界情况:
    - 限制条件:
        - 查询时间范围限制：单次查询时间跨度不超过90天
        - 查询结果数量限制：单次查询返回结果不超过10000条
        - 本地日志保留期限：适配中心本地保留近90天的操作日志
        - 数据快照大小限制：单条日志的数据快照总大小不超过10KB
    - 边界情况处理:
        - 列表为空：显示"暂无操作日志数据"的提示
        - 查询无结果：显示"未找到符合条件的操作日志"
        - 数据快照过大：截断并标注"数据过大，已截断显示"
        - 并发操作冲突：记录操作尝试和最终结果，标注冲突信息

#### 4.2.5 异常处理方案

- 查询超时或失败: 若查询日志数据量过大或数据库响应慢，应有30秒超时控制，超时后提示"查询超时，请缩小查询范围后重试"
- 网络异常: 查询请求失败时提示"网络连接失败，请检查网络后重试"
- 服务器内部错误: 显示通用错误提示"系统繁忙，请稍后重试"
- 无符合条件的日志: 列表为空时，显示"未找到符合条件的操作日志"
- 日志记录失败: 当操作日志记录失败时，不应影响业务操作的正常执行，但应记录错误日志供运维人员排查

#### 4.2.6 与其他功能的关联和依赖

- 依赖项 (Dependencies):
    - 所有需要记录操作日志的功能模块：这些模块在执行关键操作后，需调用日志服务接口记录日志
    - 权限管理模块：依赖权限配置控制日志查看访问
    - 用户管理模块：需要获取操作用户的详细信息
- 被依赖项 (Generated Dependencies):
    - 安全审计流程: 操作日志是安全审计和合规性检查的核心依据
    - 运维排障与责任认定：用于追溯问题原因和确定操作责任
    - 数据恢复：通过操作日志的数据快照辅助数据恢复工作

---
