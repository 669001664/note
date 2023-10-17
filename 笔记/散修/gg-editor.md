# gg-editor使用说明

## Editor Events
### 监听事件

```jsx
import GGEditor, { Flow } from 'gg-editor';

<GGEditor
  onBeforecommandexecute={({ command }) => {
    console.log('command', command);
  }}
>
  <Flow />
</GGEditor>
```

### 事件列表

| 事件名称 | 事件说明 |
| :--- | :--- |
| onBeforeCommandExecute | 命令执行前 |
| onAfterCommandExecute | 命令执行后 |

### 命令对象

| 命令属性 | 属性说明 | 类型 |
| :--- | :--- | :--- |
| name | 命令名称 | `string` |
| queue | 是否进入命令队列，进入命令队列则可以执行撤销、重做 | `boolean` |

## Flow
流程图
### API

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| data | 初始数据 | `object` | - |
| graph | 图配置项，参考 [G6 Graph API](https://antv.alipay.com/zh-cn/g6/1.x/api/graph.html) | `object` | - |
| align | 对齐配置 | [`object`](#Align) | - |
| grid | 网格线配置 | [`object`](#Grid) | - |
| shortcut | 快捷键配置 | [`object`](#Shortcut) | - |
| noEndEdge | 是否支持悬空边 | `boolean` | `true` |

### Align

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| line | 对齐线样式 | `object` | - |
| item | 图项对齐 | `true` `false` `horizontal` `vertical` `center` | - |
| grid | 网格对齐 | `true` `false` `cc` `tl` | - |

### Grid

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| cell | 网孔尺寸 | `number` | - |
| line | 网格线样式 | `object` | - |

### Shortcut
```jsx
  shortcut: {
    zoomIn: true,   // 开启放大快捷键
    zoomOut: false, // 开启视口缩小快捷键
  }
```

### Events
#### 事件对象

| 属性属性 | 属性说明 |
| :--- | :--- |
| action | 动作包括：`add`、`update`、`remove`、`changeData` |
| item | 图项 |
| shape | 图形 |
| x | 图横坐标 |
| y | 图纵坐标 |
| domX | dom 横坐标 |
| domY | dom 纵坐标 |
| domEvent | 原生 dom 事件 |
| currentItem | `drag` 拖动图项 |
| currentShape | `drag` 拖动图形 |
| toShape | `mouseleave`、`dragleave` 到达的图形 |
| toItem | `mouseleave`、`dragleave` 到达的图项 |

#### 组合事件

此类事件可以结合前缀 `node`、`edge`、`group`、`guide`、`anchor` 组合使用，例如：

```jsx
import GGEditor, { Flow } from 'gg-editor';

<GGEditor>
  <Flow
    onClick={() => {}}       // 点击画布
    onNodeClick={() => {}}   // 点击节点
    onEdgeClick={() => {}}   // 点击边线
    onGroupClick={() => {}}  // 点击群组
    onGuideClick={() => {}}  // 点击导引
    onAnchorClick={() => {}} // 点击锚点
  />
</GGEditor>
```

| 事件名称 | 事件说明 |
| :--- | :--- |
| onClick | 鼠标左键点击事件 |
| onDoubleClick | 鼠标左键双击事件 |
| onMouseEnter | 鼠标移入事件 |
| onMouseLeave | 鼠标移除事件 |
| onMouseDown | 鼠标按下事件 |
| onMouseUp | 鼠标抬起事件 |
| onMouseMove | 鼠标移动事件 |
| onDragStart | 鼠标开始拖拽事件 |
| onDrag | 鼠标拖拽事件 |
| onDragEnd | 鼠标拖拽结束事件 |
| onDragEnter | 鼠标拖拽进入事件 |
| onDragLeave | 鼠标拖拽移出事件 |
| onDrop | 鼠标拖拽放置事件 |
| onContextMenu | 鼠标右键菜单事件 |


#### 普通事件

| 事件名称 | 事件说明 |
| :--- | :--- |
| onMouseWheel | 鼠标滚轮事件 |
| onKeyDown | 键盘按键按下事件 |
| onKeyUp | 键盘按键抬起事件 |
| onBeforeChange | 子项数据变化前 |
| onAfterChange | 子项数据变化后 |
| onBeforeChangeSize | 画布尺寸变化前 |
| onAfterChangeSize | 画布尺寸变化后 |
| onBeforeViewportChange | 视口变化前 |
| onAfterViewportChange | 视口变化后 |
| onBeforeItemActived | 激活前 |
| onAfterItemActived | 激活后 |
| onBeforeItemInactivated | 取消激活前 |
| onAfterItemInactivated | 取消激活后 |
| onBeforeItemSelected | 选中前 |
| onAfterItemSelected | 选中后 |
| onBeforeItemUnselected | 取消选中前 |
| onAfterItemUnselected | 取消选中后 |
| onKeyUpEditLabel | 键盘按键抬起事件（节点编辑）|

## ItemPanel
元素面板栏

必需配合 `<Item />` 组件使用，如果 `<Item />` 包含 `src` 属性则自动显示元素概览图片。

```jsx
import GGEditor, { Flow, Item, ItemPanel } from 'gg-editor';

<GGEditor>
  <Flow />
  <ItemPanel>
    <Item
      type="node"
      size="72*72"
      shape="flow-circle"
      model={{
        color: '#FA8C16',
        label: '起止节点',
      }}
      src="https://gw.alipayobjects.com/zos/rmsportal/ZnPxbVjKYADMYxkTQXRi.svg"
    />
  </ItemPanel>
</GGEditor>
```

### Item API

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| type | **必填** 元素类型，可选类型：`node` `edge` | `string` | - |
| size | **必填** 元素尺寸，书写格式：`50*50` | `string` | - |
| shape | **必填** 元素形状，内置形状 | `string` | - |
| model | 元素初始 model | `object` | - |
| src | 元素概览 src | `string` | - |

## ContextMenu

右键菜单，负责菜单显示隐藏，命令按钮绑定与可用禁用状态控制。


必需配合`<Command />`组件使用

自动根据不同页面状态显示对应菜单，例如：选中节点时则只会显示 `NodeMenu`。

```jsx
import GGEditor, {
  Flow,
  Command,
  ContextMenu,
  NodeMenu,
  EdgeMenu,
  GroupMenu,
  MultiMenu,
  CanvasMenu,
} from 'gg-editor';

<GGEditor>
  <Flow />
  <ContextMenu>
    <NodeMenu>     // 节点右键菜单
      <Command name="copy">复制</Command>
      <Command name="delete">删除</Command>
    </NodeMenu>
    <EdgeMenu />   // 边线右键菜单
    <GroupMenu />  // 群组右键菜单
    <MultiMenu />  // 多选右键菜单
    <CanvasMenu /> // 画布右键菜单
  </ContextMenu>
</GGEditor>
```

## Command
命令

此组件只能嵌套在 `<Toolbar />`或 `<ContextMenu />` 组件内使用：

```jsx
import GGEditor, { Flow, Command, Toolbar, ContextMenu } from 'gg-editor';

<GGEditor>
  <Flow />
  <Toolbar>
    <Command name="undo">撤销</Command>
    <Command name="redo">重做</Command>
  </Toolbar>
  <ContextMenu>
    <Command name="undo">撤销</Command>
    <Command name="redo">重做</Command>
  </ContextMenu>
</GGEditor>
```

### API

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| name | 命令名称 | `string` | - |

### 内置命令

| 命令英文名 | 命令中文名 | 快捷键（Mac） | 快捷键（Win） | 适用页面 |
| :--- | :--- | :--- | :--- | :--- |
| clear | 清空画布 | - | - | All |
| selectAll | 全选 | `⌘A` | `Ctrl+A` | All |
| undo | 撤销 | `⌘Z` | `Ctrl + Z` | All |
| redo | 重做 | `⇧⌘Z` | `Shift + Ctrl + Z` | All |
| delete | 删除 | `Delete` | `Delete` | All |
| zoomIn | 放大 | `⌘=` | `Ctrl + =` | All |
| zoomOut | 缩小 | `⌘-` | `Ctrl + -` | All |
| autoZoom | 自适应尺寸 | - | - | All |
| resetZoom | 实际尺寸 | `⌘0` | `Ctrl + 0` | All |
| toFront | 提升层级 | - | - | All |
| toBack | 下降层级 | - | - | All |
| copy | 复制 | `⌘C` | `Ctrl + C` | Flow |
| paste | 粘贴 | `⌘V` | `Ctrl + V` | Flow |
| multiSelect | 多选模式 | - | - | Flow |
| addGroup | 成组 | `⌘G` | `Ctrl + G` | Flow |
| unGroup | 取消组 | `⇧⌘G` | `Shift + Ctrl + G` | Flow |
| append | 添加相邻节点 | `Enter` | `Enter` | Mind |
| appendChild | 添加子节点 | `Tab` | `Tab` | Mind |
| collaspeExpand | 折叠/展开 | `⌘/` | `Ctrl + /` | Mind |


## DetailPanel
属性面板栏

属性栏会自动根据不同页面状态显示对应面板，例如：选中节点时则只会显示 `NodePanel`。

```jsx
import GGEditor, {
  Flow,
  DetailPanel,
  NodePanel,
  EdgePanel,
  GroupPanel,
  MultiPanel,
  CanvasPanel,
} from 'gg-editor';

<GGEditor>
  <Flow />
  <DetailPanel>
    <NodePanel>     // 节点属性面板
      <NodeDetail />
    </NodePanel>
    <EdgePanel />   // 边线属性面板
    <GroupPanel />  // 群组属性面板
    <MultiPanel />  // 多选属性面板
    <CanvasPanel /> // 画布属性面板
  </DetailPanel>
</GGEditor>
class NodeDetail extends React.Component {
  render() {
    console.log('this.props', this.props);
  }
}
```

## Props API

```jsx
import { withPropsAPI } from 'gg-editor';

class Component extends React.Component {
  componentDidMount() {
    const { propsAPI } = this.props;

    console.log(propsAPI);
  }
}

export default withPropsAPI(Component);
```

### API

经过 `withPropsAPI` 包装的组件将会自带 `propsAPI` 属性，`propsAPI` 提供的 API 如下：

| 属性 | 说明 | 类型 |
| :--- | :--- | :--- |
| executeCommand | 执行命令 | `function(command)` |
| read | 读取数据 | `function(data)` |
| save | 保存数据 | `function() => object` |
| add | 添加图项 | `function(type, model)` |
| find | 查找图项 | `function(id)` |
| update | 更新图项 | `function(item, model)` |
| remove | 删除图项 | `function(item)` |
| getSelected | 获取当前选中图项 | `function` |

## RegisterNode
注册节点

```jsx
import GGEditor, { Flow, RegisterNode } from 'gg-editor';

<GGEditor>
  <Flow />
  <RegisterNode name={...} config={...} extend={...} />
</GGEditor>
```

### API

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| name | 节点名称 | `string` | - |
| config | 节点配置 | `object` | - |
| extend | 继承图形 | `string` | - |

### 内置节点

| 节点英文名 | 节点中文名 | 示例预览 |适用页面 |
| :--- | :--- | :--- | :--- |
| flow-circle | 起止节点 | ![起止节点](https://gw.alipayobjects.com/zos/rmsportal/ZnPxbVjKYADMYxkTQXRi.svg) | Flow |
| flow-rect | 常规节点 | ![起止节点](https://gw.alipayobjects.com/zos/rmsportal/wHcJakkCXDrUUlNkNzSy.svg) | Flow |
| flow-rhombus | 分叉节点 | ![分叉节点](https://gw.alipayobjects.com/zos/rmsportal/SnWIktArriZRWdGCnGfK.svg) | Flow |
| flow-capsule | 模型节点 | ![模型节点](https://gw.alipayobjects.com/zos/rmsportal/rQMUhHHSqwYsPwjXxcfP.svg) | Flow |

## RegisterEdge
注册边

```jsx
import GGEditor, { Flow, RegisterEdge } from 'gg-editor';

<GGEditor>
  <Flow />
  <RegisterEdge name={...} config={...} extend={...} />
</GGEditor>
```

### API

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| name | 边名称 | `string` | - |
| config | 边配置 | `object` | - |
| extend | 继承图形 | `string` | - |

### 内置边

| 边英文名 | 边中文名 | 示例预览 |适用页面 |
| :--- | :--- | :--- | :--- |
| flow-polyline | 图折线 | ![图折线](https://cdn.yuque.com/lark/2018/png/223/1522559188562-7ecad6d2-36a7-4b68-ba6e-2d0b65b594e1.png) | Flow |
| flow-polyline-round | 圆角折线 | ![圆角折线](https://cdn.yuque.com/lark/2018/png/223/1522558993675-9448ac3d-27d7-46f3-8db9-c6d1a6a35c74.png) | Flow |
| flow-smooth | 图曲线 | ![图曲线](https://cdn.yuque.com/lark/2018/png/223/1522558884115-d96bf55b-4771-4f12-8641-d552829215e1.png) | Flow |

## RegisterCommand

注册命令

```jsx
import GGEditor, { Flow, RegisterCommand } from 'gg-editor';

<GGEditor>
  <Flow />
  <RegisterCommand name={...} config={...} extend={...} />
</GGEditor>
```

### API

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| name | 命令名称 | `string` | - |
| config | 命令配置 | `object` | - |
| extend | 继承命令 | `string` | - |

```jsx
import React from "react";
import { RegisterCommand } from "gg-editor";

class CustomCommand extends React.Component {
  render() {
    const config = {
      // 是否进入列队，默认为 true
      queue: true,

      // 命令是否可用
      enable(/* editor */) {
        return true;
      },

      // 正向命令逻辑
      execute(/* editor */) {
        console.log("执行正向命令");
      },

      // 反向命令逻辑
      back(/* editor */) {
        console.log("执行反向命令");
      },

      // 快捷按键配置
      shortcutCodes: [["metaKey", "s"], ["ctrlKey", "s"]]
    };

    return <RegisterCommand name="customCommand" config={config} />;
  }
}

export default CustomCommand;
```

## Toolbar

工具栏，负责命令按钮绑定与可用禁用状态控制。

必需配合 [`<Command />`](./command.zh-CN.md) 组件使用

```jsx
import GGEditor, { Flow, Command, Toolbar } from 'gg-editor';

<GGEditor>
  <Flow />
  <Toolbar>
    <Command name="undo">撤销</Command>
    <Command name="redo">重做</Command>
  </Toolbar>
</GGEditor>
```

## Minimap
缩略图  
不指定宽高的情况下则自动适应容器尺寸

```jsx
import GGEditor, { Flow, Minimap } from 'gg-editor';

<GGEditor>
  <Flow />
  <Minimap width={200} height={200} />
</GGEditor>
```

### API

| 属性 | 说明 | 类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| container | 容器 id | `string` | - |
| width | 宽度 | `number` | - |
| height | 高度 | `number` | - |
| viewportWindowStyle | 视窗样式 | `object` | - |
| viewportBackStyle | 背景样式 | `object` | - |    


# 流程编辑器开发

#### 目录结构
![目录结构](./src/assets/icons/editor_menu.png)

#### 主页面(入口文件)

和流程图相关的组件都要包裹在`<GGEditor />`标签中

```jsx
// gg-editor2与gg-editor 2.0.4版本功能一致，只是在2.0.4版本修复了在IE、Firefox浏览器鼠标滚动报错的bug
import GGEditor, { Flow } from 'gg-editor2'; 

<GGEditor
  className={styles[`${clsPrefix}`]}
  onAfterCommandExecute={handleAfterCommandExecute}
>
  <div className={styles['item-left']}>
    <FlowItemPanel {...props} /> {/* 元素面板 */}
    <EditorMinimap miniMapRef={miniMapRef} /> {/* 缩略图 */}
  </div>
  <div className={styles['item-center']}>
    <div className={styles.editorHd}>
      <FlowToolbar /> {/* 工具栏 */}
    </div>
    <Flow
      ref={flowRef}
      className={styles.flow}
      style={{ backgroundColor: '#F8F8F8' }} // 画布背景色
      align={{ item: 'center' }} // 元素对齐方式配置
      // 网格线配置
      grid={{
        line: {
          stroke: '#DEDEDE',
          lineWidth: 0.5,
        },
        type: 'line',
      }}
      graph={{
        edgeDefaultShape: 'flow-edge', // 默认边样式设置
      }}
      noEndEdge={false} // 是否支持悬空线
      shortcut={{
        // 快捷键配置
        saveFlow: true, // 保存
        leftItem: true, // 左移
        rightItem: true, // 右移
        downItem: true, // 下移
        upItem: true, // 上移
      }}
      onAfterChange={handleAfterChange} // 子项数据变化后
      onClick={handleItemClick} // 鼠标左键点击事件
    />
  </div>
  <div className={styles['item-right']}>
    <div className={styles.editorSidebar}>
      <FlowDetailPanel /> {/* 属性面板 */}
    </div>
  </div>
  <FlowContextMenu /> {/* 画布右键菜单 */}
  <FlowEdge /> {/* 自定义边 */}
  <SaveFlowCommand onSave={handleSave} /> {/* 保存命令 */}
  <LeftItemCommand /> {/* 左移命令 */}
  <RightItemCommand /> {/* 右移命令 */}
  <DownItemCommand /> {/* 下移命令 */}
  <UpItemCommand /> {/* 上移命令 */}
</GGEditor>
```
