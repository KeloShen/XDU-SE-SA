明白了，我会在原文基础上，仅为重点词语添加英文对照，保持原有格式不变。

# 质量属性 (Quality Attributes) 与策略 (Tactics) 详解

## 概述
质量属性 (Quality Attributes, QA) 是指可用性、性能、安全性等可度量、可测试的属性，属于非功能性需求 (Non-functional Requirements)，会影响系统的运行时行为、系统设计方式以及用户的体验等。

策略 (Tactics) 是满足特定质量属性的具体措施，是软件体系结构 (Software Architecture) 中体系结构风格 (Architectural Style) 的基本单元，不同的体系结构风格包含不同的策略集合，以实现相应的质量属性。

## 1. 可用性 (Availability)

### 定义
软件在特定环境下持续正常运行的能力，即系统能够正常运行的时间比例。它关注系统是否发生了故障以及故障的后果。

### 场景组成
- **刺激源 (Source of Stimulus)**：故障的迹象（来自内部或外部）
- **刺激 (Stimulus)**：系统出错、系统崩溃、给出结果不准时、给出错误结果
- **制品 (Artifact)**：计算、存储、网络传输（系统被影响的部分）
- **环境 (Environment)**：正常状态或"亚健康"状态
- **响应 (Response)**：
  - 记录日志 (Logging)（错误报告）
  - 回传给厂家
  - 通知管理员或其他系统
  - 关闭系统
- **响应衡量指标 (Response Measure)**：
  - 故障时间百分比
  - 修复故障所需时间
  - 平均无故障时间

### 实现策略

#### 1. 故障检测 (Fault Detection)
- **监控探测 (Ping/Echo)**：监控组件不定期向被监控组件发送ping消息
- **心跳 (Heartbeat)**：被监控组件定期发送心跳信号
- **异常 (Exceptions)**：通过编程语言支持处理异常

#### 2. 故障恢复 (Fault Recovery)
- **投票 (Voting)**：通过冗余组件投票机制选取正确结果
- **主动冗余 (Active Redundancy) 和 被动冗余 (Passive Redundancy)**：确保备用系统及时接管
- **备件 (Spare)**：预留备用组件
- **影子操作 (Shadow Operation)**：运行多个副本，一个用于实际请求，其他作为"影子"模式运行
- **状态再同步 (State Resynchronization)**：使系统状态重新达到一致
- **检查点/回滚 (Checkpoint/Rollback)**：定期保存系统状态

> 解释：Shadow操作类似于A/B测试，但主要用于系统可靠性验证，而不是功能测试。

#### 3. 故障避免 (Fault Prevention)
- **服务下线 (Service Removal)**：主动下线以避免故障
- **事务 (Transaction)**：确保操作的原子性
- **进程监控 (Process Monitor)**：监控系统健康状况

## 2. 可修改性 (Modifiability)

### 定义
指软件系统在未来能够容易地进行修改的能力，以适应需求和环境变更。

### 场景组成
- **刺激源 (Source of Stimulus)**：开发人员、管理员、用户等
- **刺激 (Stimulus)**：改变项
- **制品 (Artifact)**：被改变的部分
- **环境 (Environment)**：系统可被修改的状态
- **响应 (Response)**：修改者理解并完成修改和部署
- **响应衡量指标 (Response Measure)**：
  - 修改完成时间
  - 人力/经济成本
  - 受影响元素数量

### 实现策略

#### 1. 限制修改范围 (Limit Modification Scope)
- **模块高内聚低耦合 (High Cohesion Low Coupling)**
- **使用通用化模块 (Generic Modules)**
- **隐藏信息 (Information Hiding)**
- **维持接口不变 (Interface Stability)**
- **限制通信路径 (Communication Path Limitation)**
- **使用中介 (Mediator)**
- **命名服务 (Naming Service)**

#### 2. 延迟绑定时间 (Defer Binding Time)
- **配置文件 (Configuration Files)**
- **发布/订阅模式 (Publish/Subscribe Pattern)**
- **多态 (Polymorphism)**
- **组件更换 (Component Replacement)**
- **遵守已定义的协议 (Protocol Adherence)**


> 解释：延迟绑定时间策略允许系统在运行时动态改变行为，而不需要重新编译或部署。

## 3. 性能 (Performance)

### 定义
指软件系统在给定条件下执行任务或提供服务时所展现的效率或速度，关注系统对事件的响应速度。

### 场景组成
- **刺激源 (Source of Stimulus)**：系统内部或外部（用户请求、并发用户数、数据量增加、定时事件）
- **刺激 (Stimulus)**：事件的产生（周期性、随机性、偶然性）
- **制品 (Artifact)**：系统服务
- **环境 (Environment)**：正常状态、紧急状态、过载状态等
- **响应 (Response)**：系统对事件的处理
- **响应衡量指标 (Response Measure)**：
  - 响应时间
  - 吞吐量 (Throughput)
  - 并发用户数量
  - 失败率
  - 处理时长

### 实现策略

#### 1. 优化资源需求 (Resource Demand Optimization)
- **提高计算效率 (Computational Efficiency)**：优化算法和代码实现
- **减少要处理的数据总量 (Data Volume Reduction)**：数据过滤、压缩
- **限制执行时间 (Execution Time Limitation)**
- **限制待处理事件队列长度 (Queue Size Limitation)**

> 解释：就像地铁限流一样，系统也需要根据自身承载能力来限制并发请求数量。

#### 2. 优化资源管理 (Resource Management Optimization)
- **引入并发机制 (Concurrency)**
- **增加可用资源 (Resource Increase)**：增加硬件资源、带宽等
- **维持数据或计算的多个副本 (Multiple Copies)**：使用缓存

#### 3. 优化资源仲裁 (Resource Arbitration)
- **先来先服务 (First-Come-First-Served, FCFS)**
- **固定优先级调度 (Fixed Priority Scheduling)**
- **动态优先级调度 (Dynamic Priority Scheduling)**
- **静态调度 (Static Scheduling)**

## 4. 安全性 (Security)

### 定义
软件在受到恶意攻击的情况下仍能继续正确运行，并确保软件在授权范围内被合法使用的能力。

### 场景组成
- **刺激源 (Source of Stimulus)**：外部攻击者/内部员工
- **刺激 (Stimulus)**：任何对系统造成威胁的行为
- **制品 (Artifact)**：系统对外提供的服务/数据
- **环境 (Environment)**：联网或未联网、在线或离线、在防火墙内或外
- **响应衡量指标 (Response Measure)**：
  - 发起攻击的难度
  - 从攻击中恢复的难度
  - 攻击检测概率
  - 服务可用性百分比

### 实现策略

#### 1. 抵抗攻击 (Attack Resistance)
- **验证用户身份 (Authentication)**：账号密码+验证码
- **验证用户权限 (Authorization)**：角色权限管理
- **维持数据保密性 (Data Confidentiality)**：如HTTPS加密
- **维持数据完整性 (Data Integrity)**：如校验码验证
- **减少暴露 (Exposure Reduction)**：关闭不必要端口
- **限制访问 (Access Restriction)**：防火墙配置

#### 2. 检测攻击 (Attack Detection)
- **安全日志 (Security Logging)**：记录操作和IP地址
- **异常行为监测 (Anomaly Detection)**：使用机器学习等技术

#### 3. 从攻击中恢复 (Attack Recovery)
- **恢复状态 (State Recovery)**：使用缓存恢复
- **识别攻击者 (Attacker Identification)**

## 5. 可测试性 (Testability)

### 定义
软件被测试的难易程度，即通过测试发现并证明错误的轻松程度。

### 场景组成
- **刺激源 (Source of Stimulus)**：各类测试人员、开发者
- **刺激 (Stimulus)**：开发里程碑完成、正常/异常输入
- **制品 (Artifact)**：系统模块、组件或整体
- **环境 (Environment)**：各个开发阶段
- **响应衡量指标 (Response Measure)**：
  - 功能正确性指标
  - 测试覆盖率 (Test Coverage)
  - 未来发现bug概率
  - 测试时间

### 实现策略

#### 1. 黑盒测试 (Black-box Testing)
- **录制/回放 (Record/Playback)**：记录用户操作序列
- **分离接口和实现 (Interface-Implementation Separation)**：便于跨平台测试
- **提供专用测试路径 (Dedicated Test Path)**：如安卓的"开发者选项"

#### 2. 白盒测试 (White-box Testing)
- **使用IDE内置调试工具 (IDE Debugging Tools)**：断点、单步执行等
- **使用外部工具 (External Testing Tools)**：专门的测试工具

## 6. 易用性 (Usability)

### 定义
用户能够方便地使用软件系统的程度。

### 场景组成
- **刺激源 (Source of Stimulus)**：用户操作、系统事件
- **刺激 (Stimulus)**：各类用户操作和需求
- **响应衡量指标 (Response Measure)**：
  - 任务完成时间
  - 错误次数
  - 用户满意度
  - 操作成功率

### 实现策略

#### 1. 运行时策略 (Runtime Tactics)
- **猜测任务 (Task Prediction)**：预测用户意图
- **适当反馈 (Appropriate Feedback)**：及时提供提示
- **一致体验 (Consistent Experience)**：PC端和移动端保持一致
- **支持撤销 (Support Undo)**：允许操作回退
- **操作引导 (Operation Guide)**：提供清晰指南
- **简化操作 (Operation Simplification)**：减少操作步骤

#### 2. 设计时策略 (Design-time Tactics)
- **用户界面独立 (UI Independence)**：提供多种主题
- **MVC模式 (Model-View-Controller)**：分离数据、表示和控制
- **PAC模式 (Presentation-Abstraction-Control)**：强调分层抽象
- **用户界面架构 (UI Architecture)**：Seeheim和Arch/Slinky

> 解释：这些架构模式（MVC、PAC等）不仅提高了系统的可维护性，也能让用户界面更容易适应不同的使用场景和用户需求。
