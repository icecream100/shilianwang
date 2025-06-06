# 基于Element Plus的UI开发规范文档

## 1. 概述

本文档基于Element Plus组件库的设计语言和视觉规范，制定了标准化的UI开发规范，用于指导AI生成现代化、一致性的产品功能架构图和界面设计。本规范遵循Element Plus的设计原则：简洁、一致、高效。

## 2. 设计原则

### 2.1 核心理念
- **一致性 Consistency**：与Element Plus保持一致的设计语言
- **反馈 Feedback**：通过界面样式变化和交互动效为用户提供反馈
- **效率 Efficiency**：简化用户的工作流程，提升操作效率
- **可控 Controllability**：用户可以自由控制自己的操作

### 2.2 视觉层次
- **主要信息**：使用主色调突出显示
- **次要信息**：使用中性色调
- **辅助信息**：使用浅色调或灰色
- **警示信息**：使用警告色或危险色

## 3. 配色规范（基于Element Plus色彩体系）

### 3.1 主色调（Primary Colors）
- **主品牌色**：#409EFF（Element Plus主蓝色）
- **主色浅色**：#79BBFF
- **主色深色**：#337ECC
- **主色超浅**：#ECF5FF
- **主色超深**：#1D39C4

### 3.2 功能色彩（Functional Colors）
- **成功色**：#67C23A（绿色）
- **警告色**：#E6A23C（橙色）
- **危险色**：#F56C6C（红色）
- **信息色**：#909399（灰色）

### 3.3 中性色彩（Neutral Colors）
- **主要文字**：#303133
- **常规文字**：#606266
- **次要文字**：#909399
- **占位文字**：#C0C4CC
- **边框颜色**：#DCDFE6
- **分割线**：#E4E7ED
- **背景色**：#F2F6FC

### 3.4 渐变效果
- **主色渐变**：linear-gradient(135deg, #409EFF 0%, #79BBFF 100%)
- **成功渐变**：linear-gradient(135deg, #67C23A 0%, #85CE61 100%)
- **警告渐变**：linear-gradient(135deg, #E6A23C 0%, #EEBC6C 100%)

## 4. 整体布局规范

### 4.1 栅格系统
- **基础栅格**：采用24栅格系统（与Element Plus一致）
- **响应式断点**：xs(<768px), sm(≥768px), md(≥992px), lg(≥1200px), xl(≥1920px)
- **间距规范**：基础间距单位为4px，常用间距为8px、12px、16px、20px、24px

### 4.2 容器布局
- **主容器**：最大宽度1200px，居中对齐，左右padding 20px
- **卡片容器**：使用Element Plus Card组件样式，圆角4px
- **分组容器**：使用浅色背景区分不同功能区域

### 4.3 层级结构
- **页面层级**：页面 > 区块 > 组件 > 元素
- **视觉层级**：通过颜色、大小、间距建立清晰的信息层次
- **Z-index层级**：遵循Element Plus的层级规范

## 5. 组件库规范（基于Element Plus）

### 5.1 按钮组件
```css
/* 主要按钮 */
.el-button--primary {
  background-color: #409EFF;
  border-color: #409EFF;
  color: #FFFFFF;
}

/* 成功按钮 */
.el-button--success {
  background-color: #67C23A;
  border-color: #67C23A;
  color: #FFFFFF;
}

/* 警告按钮 */
.el-button--warning {
  background-color: #E6A23C;
  border-color: #E6A23C;
  color: #FFFFFF;
}

/* 危险按钮 */
.el-button--danger {
  background-color: #F56C6C;
  border-color: #F56C6C;
  color: #FFFFFF;
}
```

### 5.2 卡片组件
```css
.el-card {
  border: 1px solid #EBEEF5;
  border-radius: 4px;
  background-color: #FFFFFF;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  transition: all 0.3s;
}

.el-card:hover {
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.15);
}

.el-card__header {
  padding: 18px 20px;
  border-bottom: 1px solid #EBEEF5;
  background-color: #FAFAFA;
  font-weight: 500;
  color: #303133;
}

.el-card__body {
  padding: 20px;
}
```

### 5.3 功能模块组件
```css
.function-module {
  background: linear-gradient(135deg, #409EFF 0%, #79BBFF 100%);
  border: 1px solid #DCDFE6;
  border-radius: 4px;
  padding: 16px 20px;
  margin: 8px;
  color: #FFFFFF;
  font-size: 14px;
  font-weight: 500;
  text-align: center;
  min-width: 120px;
  min-height: 40px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
  transition: all 0.3s;
  cursor: pointer;
}

.function-module:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15), 0 0 8px rgba(0, 0, 0, 0.06);
}
```

### 5.4 次级功能组件
```css
.sub-function-module {
  background: #FFFFFF;
  border: 1px solid #DCDFE6;
  border-radius: 4px;
  padding: 12px 16px;
  margin: 6px;
  color: #606266;
  font-size: 13px;
  font-weight: 400;
  text-align: center;
  min-width: 100px;
  min-height: 36px;
  transition: all 0.3s;
  cursor: pointer;
}

.sub-function-module:hover {
  border-color: #409EFF;
  color: #409EFF;
  background-color: #ECF5FF;
}
```

### 5.5 状态指示组件
```css
.status-success {
  background: linear-gradient(135deg, #67C23A 0%, #85CE61 100%);
  color: #FFFFFF;
}

.status-warning {
  background: linear-gradient(135deg, #E6A23C 0%, #EEBC6C 100%);
  color: #FFFFFF;
}

.status-danger {
  background: linear-gradient(135deg, #F56C6C 0%, #F78989 100%);
  color: #FFFFFF;
}

.status-info {
  background: #F4F4F5;
  color: #909399;
  border: 1px solid #E4E7ED;
}
```

### 5.6 容器组件
```css
.layer-container {
  border: 1px solid #DCDFE6;
  border-radius: 4px;
  padding: 20px;
  margin: 16px 0;
  background: #FFFFFF;
  position: relative;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}

.layer-label {
  position: absolute;
  left: 20px;
  top: -10px;
  background: #409EFF;
  color: #FFFFFF;
  padding: 4px 12px;
  font-size: 12px;
  font-weight: 500;
  border-radius: 2px;
  line-height: 1;
}
```

## 6. 字体规范（基于Element Plus字体系统）

### 6.1 字体族
- **中文字体**："Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "微软雅黑", Arial, sans-serif
- **英文字体**："Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", Arial, sans-serif
- **等宽字体**：Menlo, Monaco, Consolas, "Courier New", monospace

### 6.2 字体大小层级
- **特大标题**：20px（font-size-extra-large）
- **大标题**：18px（font-size-large）
- **中标题**：16px（font-size-medium）
- **基础文字**：14px（font-size-base）
- **小文字**：13px（font-size-small）
- **超小文字**：12px（font-size-extra-small）

### 6.3 字重规范
- **常规**：400（font-weight-normal）
- **中等**：500（font-weight-medium）
- **加粗**：600（font-weight-bold）

### 6.4 行高规范
- **紧凑行高**：1.3（line-height-tight）
- **基础行高**：1.5（line-height-base）
- **宽松行高**：1.7（line-height-loose）

## 7. 间距规范（基于Element Plus间距系统）

### 7.1 基础间距单位
- **基础单位**：4px
- **常用间距**：4px, 8px, 12px, 16px, 20px, 24px, 32px, 40px

### 7.2 组件间距
- **组件外边距**：16px（margin-base）
- **组件内边距**：20px（padding-base）
- **紧凑内边距**：12px（padding-small）
- **宽松内边距**：24px（padding-large）

### 7.3 布局间距
- **页面边距**：20px
- **区块间距**：24px
- **卡片间距**：16px
- **元素间距**：8px

### 7.4 圆角规范
- **基础圆角**：4px（border-radius-base）
- **小圆角**：2px（border-radius-small）
- **圆形**：50%（border-radius-circle）

## 8. 交互规范（基于Element Plus交互标准）

### 8.1 动画时长
- **快速动画**：0.1s
- **基础动画**：0.3s
- **慢速动画**：0.5s

### 8.2 缓动函数
- **标准缓动**：cubic-bezier(0.4, 0, 0.2, 1)
- **进入缓动**：cubic-bezier(0, 0, 0.2, 1)
- **退出缓动**：cubic-bezier(0.4, 0, 1, 1)

### 8.3 悬停效果
```css
.interactive-element:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.el-button:hover {
  opacity: 0.8;
  transition: opacity 0.3s;
}
```

### 8.4 点击效果
```css
.interactive-element:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12);
  transition: all 0.1s;
}

.el-button:active {
  opacity: 0.9;
}
```

### 8.5 焦点状态
```css
.interactive-element:focus {
  outline: 2px solid #409EFF;
  outline-offset: 2px;
}

.el-input:focus {
  border-color: #409EFF;
  box-shadow: 0 0 0 2px rgba(64, 158, 255, 0.2);
}
```

## 9. 响应式设计（基于Element Plus响应式系统）

### 9.1 断点设置
- **xs**：<768px（超小屏幕，手机）
- **sm**：≥768px（小屏幕，平板）
- **md**：≥992px（中等屏幕，桌面显示器）
- **lg**：≥1200px（大屏幕，大桌面显示器）
- **xl**：≥1920px（超大屏幕）

### 9.2 栅格响应式
```css
/* 超小屏幕 */
@media (max-width: 767px) {
  .el-col-xs-24 { width: 100%; }
  .el-col-xs-12 { width: 50%; }
}

/* 小屏幕 */
@media (min-width: 768px) {
  .el-col-sm-24 { width: 100%; }
  .el-col-sm-12 { width: 50%; }
  .el-col-sm-8 { width: 33.33%; }
}

/* 中等屏幕 */
@media (min-width: 992px) {
  .el-col-md-6 { width: 25%; }
  .el-col-md-8 { width: 33.33%; }
  .el-col-md-12 { width: 50%; }
}
```

### 9.3 组件响应式适配
- **xs屏幕**：单列布局，组件全宽
- **sm屏幕**：双列布局，适当缩小间距
- **md屏幕**：三列布局，标准间距
- **lg屏幕**：四列布局，宽松间距
- **xl屏幕**：保持最佳视觉效果

## 10. 图标规范（基于Element Plus图标系统）

### 10.1 图标库
- **推荐使用**：Element Plus Icons（@element-plus/icons-vue）
- **备选方案**：Heroicons、Lucide、Tabler Icons
- **图标格式**：SVG矢量图标

### 10.2 图标尺寸
- **超小图标**：12px
- **小图标**：14px
- **标准图标**：16px
- **大图标**：20px
- **超大图标**：24px

### 10.3 图标颜色
- **主要图标**：#303133
- **次要图标**：#606266
- **禁用图标**：#C0C4CC
- **品牌图标**：#409EFF
- **状态图标**：对应状态色

### 10.4 常用图标映射
```css
.icon-database { /* 数据库 */ }
.icon-server { /* 服务器 */ }
.icon-network { /* 网络 */ }
.icon-device { /* 设备 */ }
.icon-api { /* API接口 */ }
.icon-security { /* 安全 */ }
.icon-monitor { /* 监控 */ }
.icon-analytics { /* 分析 */ }
```

## 11. 连接线规范（基于Element Plus设计语言）

### 11.1 连接线样式
```css
.connection-line {
  stroke: #DCDFE6;
  stroke-width: 1px;
  fill: none;
  stroke-dasharray: none;
}

.connection-line--primary {
  stroke: #409EFF;
  stroke-width: 2px;
}

.connection-line--dashed {
  stroke-dasharray: 5,5;
}

.connection-arrow {
  stroke: #409EFF;
  stroke-width: 2px;
  fill: #409EFF;
}
```

### 11.2 流程连接线
```css
.flow-line {
  stroke: #909399;
  stroke-width: 1px;
  marker-end: url(#arrow-marker);
}

.flow-line--active {
  stroke: #409EFF;
  stroke-width: 2px;
  animation: flow-animation 2s infinite;
}

@keyframes flow-animation {
  0% { stroke-dasharray: 0, 10; }
  100% { stroke-dasharray: 10, 0; }
}
```

### 11.3 箭头标记
```svg
<defs>
  <marker id="arrow-marker" markerWidth="10" markerHeight="10" 
          refX="9" refY="3" orient="auto" markerUnits="strokeWidth">
    <path d="M0,0 L0,6 L9,3 z" fill="#409EFF"/>
  </marker>
</defs>
```

## 12. 阴影效果（基于Element Plus阴影系统）

### 12.1 阴影层级
```css
/* 基础阴影 */
.shadow-base {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}

/* 浅阴影 */
.shadow-light {
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

/* 深阴影 */
.shadow-dark {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}
```

### 12.2 交互阴影
```css
/* 悬停阴影 */
.shadow-hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: box-shadow 0.3s;
}

/* 激活阴影 */
.shadow-active {
  box-shadow: 0 0 0 2px rgba(64, 158, 255, 0.2);
}
```

### 12.3 特殊阴影
```css
/* 成功状态阴影 */
.shadow-success {
  box-shadow: 0 0 0 2px rgba(103, 194, 58, 0.2);
}

/* 警告状态阴影 */
.shadow-warning {
  box-shadow: 0 0 0 2px rgba(230, 162, 60, 0.2);
}

/* 危险状态阴影 */
.shadow-danger {
  box-shadow: 0 0 0 2px rgba(245, 108, 108, 0.2);
}
```

## 13. 实施要求（基于Element Plus开发标准）

### 13.1 技术栈要求
- **框架**：Vue 3 + Element Plus
- **构建工具**：Vite 或 Webpack 5+
- **CSS预处理器**：SCSS/SASS（推荐）
- **包管理器**：npm 或 yarn
- **TypeScript**：推荐使用，提升代码质量

### 13.2 代码规范
- **命名规范**：遵循BEM方法论
- **CSS组织**：使用SCSS模块化管理
- **变量管理**：使用CSS自定义属性
- **注释规范**：关键样式必须添加注释
- **代码格式化**：使用Prettier统一格式

### 13.3 兼容性要求
- **现代浏览器**：Chrome 85+, Firefox 78+, Safari 14+, Edge 85+
- **移动端**：iOS Safari 14+, Chrome Mobile 85+
- **响应式支持**：完整支持所有断点
- **无障碍访问**：符合WCAG 2.1 AA标准

### 13.4 性能要求
- **首屏加载**：< 3秒
- **CSS文件大小**：< 100KB（压缩后）
- **图标资源**：使用SVG或Icon Font
- **动画性能**：60fps流畅动画
- **内存占用**：合理控制DOM节点数量

## 14. 示例模板（Vue 3 + Element Plus）

### 14.1 Vue组件示例
```vue
<template>
  <div class="architecture-diagram">
    <el-container>
      <el-main>
        <!-- 应用层 -->
        <el-card class="layer-container" shadow="hover">
          <template #header>
            <div class="layer-header">
              <el-tag type="primary" size="small">应用层</el-tag>
              <span class="layer-title">业务应用模块</span>
            </div>
          </template>
          <el-row :gutter="16">
            <el-col :xs="24" :sm="12" :md="8" v-for="module in appModules" :key="module.id">
              <div class="function-module" @click="handleModuleClick(module)">
                <el-icon><component :is="module.icon" /></el-icon>
                <span>{{ module.name }}</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
        
        <!-- 平台层 -->
        <el-card class="layer-container" shadow="hover">
          <template #header>
            <div class="layer-header">
              <el-tag type="success" size="small">平台层</el-tag>
              <span class="layer-title">平台服务</span>
            </div>
          </template>
          <el-row :gutter="12">
            <el-col :xs="12" :sm="8" :md="6" v-for="service in platformServices" :key="service.id">
              <div class="sub-function-module">
                <el-icon><component :is="service.icon" /></el-icon>
                <span>{{ service.name }}</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
      </el-main>
    </el-container>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ElCard, ElContainer, ElMain, ElRow, ElCol, ElTag, ElIcon } from 'element-plus'

interface Module {
  id: string
  name: string
  icon: string
  status?: 'success' | 'warning' | 'danger'
}

const appModules = ref<Module[]>([
  { id: '1', name: '用户管理', icon: 'User' },
  { id: '2', name: '权限控制', icon: 'Lock' },
  { id: '3', name: '数据分析', icon: 'DataAnalysis' }
])

const platformServices = ref<Module[]>([
  { id: '1', name: 'API网关', icon: 'Connection' },
  { id: '2', name: '消息队列', icon: 'Message' },
  { id: '3', name: '缓存服务', icon: 'Coin' }
])

const handleModuleClick = (module: Module) => {
  console.log('点击模块:', module.name)
}
</script>
```

### 14.2 SCSS样式示例
```scss
// 变量定义
:root {
  // Element Plus主题色
  --el-color-primary: #409EFF;
  --el-color-success: #67C23A;
  --el-color-warning: #E6A23C;
  --el-color-danger: #F56C6C;
  --el-color-info: #909399;
  
  // 自定义变量
  --architecture-spacing: 16px;
  --architecture-border-radius: 4px;
  --architecture-shadow: 0 2px 4px rgba(0, 0, 0, 0.12);
}

.architecture-diagram {
  padding: var(--architecture-spacing);
  background-color: var(--el-bg-color-page);
  
  .layer-container {
    margin-bottom: var(--architecture-spacing);
    
    .layer-header {
      display: flex;
      align-items: center;
      gap: 12px;
      
      .layer-title {
        font-size: var(--el-font-size-medium);
        font-weight: var(--el-font-weight-primary);
        color: var(--el-text-color-primary);
      }
    }
  }
  
  .function-module {
    @include module-base;
    background: linear-gradient(135deg, var(--el-color-primary) 0%, #79BBFF 100%);
    color: var(--el-color-white);
    
    &:hover {
      transform: translateY(-2px);
      box-shadow: var(--el-box-shadow-light);
    }
  }
  
  .sub-function-module {
    @include module-base;
    background: var(--el-color-white);
    border: 1px solid var(--el-border-color);
    color: var(--el-text-color-regular);
    
    &:hover {
      border-color: var(--el-color-primary);
      color: var(--el-color-primary);
      background-color: var(--el-color-primary-light-9);
    }
  }
}

// 混入
@mixin module-base {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 16px;
  border-radius: var(--architecture-border-radius);
  cursor: pointer;
  transition: all var(--el-transition-duration);
  min-height: 48px;
  text-align: center;
  font-size: var(--el-font-size-base);
  font-weight: var(--el-font-weight-primary);
}
```

### 14.3 TypeScript类型定义
```typescript
// types/architecture.ts
export interface ArchitectureModule {
  id: string
  name: string
  description?: string
  icon: string
  status: 'active' | 'inactive' | 'error' | 'warning'
  children?: ArchitectureModule[]
}

export interface ArchitectureLayer {
  id: string
  name: string
  type: 'application' | 'platform' | 'infrastructure' | 'data'
  modules: ArchitectureModule[]
  color?: string
}

export interface ArchitectureDiagram {
  id: string
  title: string
  description?: string
  layers: ArchitectureLayer[]
  connections?: Connection[]
}

export interface Connection {
  from: string
  to: string
  type: 'data' | 'api' | 'event'
  bidirectional?: boolean
}
```

## 15. 质量检查清单

### 15.1 设计一致性
- [ ] 使用Element Plus标准色彩体系
- [ ] 遵循Element Plus组件设计规范
- [ ] 保持视觉层次清晰
- [ ] 间距使用统一的基础单位

### 15.2 用户体验
- [ ] 响应式设计在所有设备上正常工作
- [ ] 交互反馈及时且明确
- [ ] 加载状态和错误状态处理完善
- [ ] 支持键盘导航和屏幕阅读器

### 15.3 技术质量
- [ ] 代码结构清晰，组件化程度高
- [ ] TypeScript类型定义完整
- [ ] 性能指标达到要求
- [ ] 跨浏览器兼容性测试通过

### 15.4 维护性
- [ ] 文档完整，注释清晰
- [ ] 样式变量化，易于主题定制
- [ ] 组件可复用性强
- [ ] 遵循团队代码规范

