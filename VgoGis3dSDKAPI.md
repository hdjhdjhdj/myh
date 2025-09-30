## Classes

<dl>
<dt><a href="#MapCore">MapCore</a></dt>
<dd><p>地图核心控制类，负责初始化和管理3D地图场景
集成了天地图服务和地形数据，提供地图基础操作能力</p>
</dd>
</dl>

## Objects

<dl>
<dt><a href="#VgoGis3dSDK">VgoGis3dSDK</a> : <code>object</code></dt>
<dd><p>SDK 命名空间</p>
</dd>
</dl>

<a name="MapCore"></a>

## MapCore

地图核心控制类，负责初始化和管理 3D 地图场景
集成了天地图服务和地形数据，提供地图基础操作能力

**Kind**: global class  
**Author:**: 匿名  
**Createtime:**: 2025-9-29 18:00

- [MapCore](#MapCore)
  - [new MapCore(domId, options)](#new_MapCore_new)
  - [.domId](#MapCore+domId) : <code>string</code>
  - [.viewer](#MapCore+viewer) : <code>Cesium.Viewer</code> \| <code>null</code>
  - [.centerLongitude](#MapCore+centerLongitude) : <code>number</code>
  - [.centerLatitude](#MapCore+centerLatitude) : <code>number</code>
  - [.centerHeight](#MapCore+centerHeight) : <code>number</code>
  - [.mapType](#MapCore+mapType) : [<code>MapTypes</code>](#MapTypes)
  - [.handler](#MapCore+handler) : <code>Cesium.ScreenSpaceEventHandler</code> \| <code>null</code>
  - [.getLevelHeight(l)](#MapCore+getLevelHeight) ⇒ <code>number</code>
  - [.initViewer()](#MapCore+initViewer) ⇒ <code>void</code>
  - [.initMap()](#MapCore+initMap) ⇒ <code>Promise.&lt;void&gt;</code>
  - [.destroyMap()](#MapCore+destroyMap) ⇒ <code>void</code>
  - [.setTdtMap()](#MapCore+setTdtMap) ⇒ <code>void</code>
  - [.setTdtElectronicMap()](#MapCore+setTdtElectronicMap) ⇒ <code>void</code>
  - [.setTdtTerrain()](#MapCore+setTdtTerrain) ⇒ <code>Promise.&lt;void&gt;</code>
  - [.changeMap()](#MapCore+changeMap) ⇒ <code>void</code>
  - [.initPreviewEvent()](#MapCore+initPreviewEvent)
  - [.load3dtilesetModel(url, [options])](#MapCore+load3dtilesetModel) ⇒ <code>Promise.&lt;void&gt;</code>
  - [.flyTo(options)](#MapCore+flyTo)
  - [.setView(options)](#MapCore+setView)
  - [.zoomIn([rate])](#MapCore+zoomIn)
  - [.zoomOut([rate])](#MapCore+zoomOut)
  - [.getMapCenter([car3])](#MapCore+getMapCenter) ⇒ <code>Array</code>
  - [.handleColor([color])](#MapCore+handleColor) ⇒ <code>Cesium.Color</code>
  - [.getLineMaterial(lineType, [opts])](#MapCore+getLineMaterial) ⇒ <code>Cesium.Material</code>
  - [.addPoint(options)](#MapCore+addPoint) ⇒ <code>Cesium.Entity</code>
  - [.addPolygon(pos, opts)](#MapCore+addPolygon) ⇒ <code>Cesium.Entity</code>
  - [.remove()](#MapCore+remove)
  - [.removeById()](#MapCore+removeById)
  - [.removeAll()](#MapCore+removeAll)
  - [.getById(id)](#MapCore+getById) ⇒ <code>Cesium.Entity</code> \| <code>null</code>
  - [.showEntityById(id, show)](#MapCore+showEntityById)
  - [.zoomToEntityById(id)](#MapCore+zoomToEntityById)
  - [.flyToEntityById(id)](#MapCore+flyToEntityById)
  - [.addPointSurveillance([opts])](#MapCore+addPointSurveillance) ⇒ <code>Cesium.Entity</code> \| <code>null</code>
  - [.removePointSurveillance(id)](#MapCore+removePointSurveillance)
  - [.removePointSurveillanceAll()](#MapCore+removePointSurveillanceAll)
  - [.showPointSurveillance(id, [show])](#MapCore+showPointSurveillance)
  - [.showPointSurveillanceAll([show])](#MapCore+showPointSurveillanceAll)
  - [.addPolygonHouse([opts])](#MapCore+addPolygonHouse) ⇒ <code>Cesium.Entity</code> \| <code>null</code>
  - [.removePolygonHouse(id)](#MapCore+removePolygonHouse)
  - [.removePolygonHouseAll()](#MapCore+removePolygonHouseAll)
  - [.showPolygonHouse(id, [show])](#MapCore+showPolygonHouse)
  - [.showPolygonHouseAll([show])](#MapCore+showPolygonHouseAll)

<a name="new_MapCore_new"></a>

### new MapCore(domId, options)

MapCore.constructor 创建实例

| Param                         | Type                 | Description                               |
| ----------------------------- | -------------------- | ----------------------------------------- |
| domId                         | <code>String</code>  | div 元素的 id 必需                        |
| options                       | <code>Object</code>  | 配置项 必需                               |
| options.tdtKey                | <code>String</code>  | 天地图 key 必需                           |
| options.zoom                  | <code>Number</code>  | 地图放大层级，取值范围[1-30] 默认 29 可选 |
| options.isFlyCenter           | <code>Boolean</code> | 是否定位到地图中心点 默认 false 可选      |
| options.preserveDrawingBuffer | <code>Boolean</code> | 是否允许截图 默认 false 可选              |

**Example**

```js
// 初始化地图核心实例 传入DOM容器ID初始化地图
const gismap = new VgoGis3dSDK.MapCore('cesiummap-container', { tdtKey: 'b82178083e4eb37ab96e262d5c1ef8ad' }, () => {})
```

<a name="MapCore+domId"></a>

### mapCore.domId : <code>string</code>

地图渲染的 DOM 容器 ID
地图将被渲染到该 ID 对应的 DOM 元素中

**Kind**: instance property of [<code>MapCore</code>](#MapCore)  
**Access**: public  
<a name="MapCore+viewer"></a>

### mapCore.viewer : <code>Cesium.Viewer</code> \| <code>null</code>

地图视图控制器实例
通常为 Cesium.Viewer 对象，提供地图交互的核心能力

**Kind**: instance property of [<code>MapCore</code>](#MapCore)  
**Access**: public  
<a name="MapCore+centerLongitude"></a>

### mapCore.centerLongitude : <code>number</code>

地图初始中心点的经度
采用 WGS84 坐标系，单位：度

**Kind**: instance property of [<code>MapCore</code>](#MapCore)  
**Default**: <code>102.788435</code>  
**Access**: public  
<a name="MapCore+centerLatitude"></a>

### mapCore.centerLatitude : <code>number</code>

地图初始中心点的纬度
采用 WGS84 坐标系，单位：度

**Kind**: instance property of [<code>MapCore</code>](#MapCore)  
**Default**: <code>35.799272</code>  
**Access**: public  
<a name="MapCore+centerHeight"></a>

### mapCore.centerHeight : <code>number</code>

地图初始视角高度
单位：米

**Kind**: instance property of [<code>MapCore</code>](#MapCore)  
**Default**: <code>600</code>  
**Access**: public  
<a name="MapCore+mapType"></a>

### mapCore.mapType : [<code>MapTypes</code>](#MapTypes)

地图默认图层类型
决定初始化时加载的底图样式

**Kind**: instance property of [<code>MapCore</code>](#MapCore)  
**Default**: <code>MapTypes.SATELLITE</code>  
**Access**: public  
<a name="MapCore+handler"></a>

### mapCore.handler : <code>Cesium.ScreenSpaceEventHandler</code> \| <code>null</code>

地图事件处理器
用于管理鼠标、键盘等交互事件

**Kind**: instance property of [<code>MapCore</code>](#MapCore)  
**Access**: public  
<a name="MapCore+getLevelHeight"></a>

### mapCore.getLevelHeight(l) ⇒ <code>number</code>

获取地图层级对应的高度值

根据地图的层级计算并返回对应的高度，层级范围为 1 到 30，
层级数值越小，返回的高度值越大；层级数值越大，返回的高度值越小

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>number</code> - 计算得到的高度值，单位未指定

| Param | Type                | Description                         |
| ----- | ------------------- | ----------------------------------- |
| l     | <code>number</code> | 地图层级，必须是 1 到 30 之间的整数 |

**Example**

```js
// 返回 200 + 400*(30-1) = 200 + 11600 = 11800
getLevelHeight(1)
```

**Example**

```js
// 返回 200 + 400*(30-30) = 200 + 0 = 200
getLevelHeight(30)
```

<a name="MapCore+initViewer"></a>

### mapCore.initViewer() ⇒ <code>void</code>

主要配置包括：

- 禁用默认的 accessToken 检查和在线底图加载
- 关闭多种不必要的 UI 控件（如全屏按钮、地理编码器、首页按钮等）
- 配置场景渲染参数（抗锯齿、帧率显示、水雾特效等）
- 移除默认的双击事件行为
- 隐藏 Cesium 品牌标识
- 可配置截图所需的绘图缓冲区保留选项

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>void</code> - 无返回值  
<a name="MapCore+initMap"></a>

### mapCore.initMap() ⇒ <code>Promise.&lt;void&gt;</code>

初始化地图的方法

该方法是地图初始化的入口，依次执行天地图图层设置、地形设置和预览事件初始化，
确保地图组件按正确顺序加载必要资源和事件监听

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Promise.&lt;void&gt;</code> - 无返回值，通过异步方式完成地图初始化
注：方法使用 async/await 确保地形加载完成后再进行后续操作，保证初始化顺序性  
<a name="MapCore+destroyMap"></a>

### mapCore.destroyMap() ⇒ <code>void</code>

销毁流程包括以下步骤：

1. 移除所有事件监听
2. 清除所有图层或叠加物
3. 若存在 3D 瓦片集(#tileset3d)，则销毁该瓦片集
4. 销毁 Cesium viewer 实例，释放核心地图资源

注：在组件卸载或不再需要地图功能时，应调用此方法进行完整清理

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>void</code> - 无返回值  
<a name="MapCore+setTdtMap"></a>

### mapCore.setTdtMap() ⇒ <code>void</code>

设置天地图卫星地图图层

该方法用于向 Cesium viewer 添加天地图的卫星影像图层及其注记图层，
实现基于天地图服务的卫星地图显示

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>void</code> - 无返回值  
<a name="MapCore+setTdtElectronicMap"></a>

### mapCore.setTdtElectronicMap() ⇒ <code>void</code>

设置天地图电子地图图层

该方法用于向 Cesium viewer 添加天地图的电子矢量地图图层及其注记图层，
实现基于天地图服务的电子地图显示

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>void</code> - 无返回值  
<a name="MapCore+setTdtTerrain"></a>

### mapCore.setTdtTerrain() ⇒ <code>Promise.&lt;void&gt;</code>

异步设置天地图地形数据

该方法用于加载并配置天地图的地形服务，为地图添加三维地形效果，
支持水面掩膜和顶点法线计算，提升地形渲染的真实感

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Promise.&lt;void&gt;</code> - 无返回值，通过异步方式加载地形数据  
<a name="MapCore+changeMap"></a>

### mapCore.changeMap() ⇒ <code>void</code>

切换卫星地图与电子街道地图

该方法用于在卫星地图和电子街道地图之间进行切换，通过先移除现有天地图图层，
再根据当前地图类型加载对应类型的地图图层，并更新地图类型标识

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>void</code> - 无返回值  
<a name="MapCore+initPreviewEvent"></a>

### mapCore.initPreviewEvent()

初始化鼠标监听事件

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
<a name="MapCore+load3dtilesetModel"></a>

### mapCore.load3dtilesetModel(url, [options]) ⇒ <code>Promise.&lt;void&gt;</code>

加载 3D Tiles 模型并添加到地图场景中

该方法用于异步加载 3D Tiles 格式的模型数据，支持通过配置项自定义加载参数，
加载完成后将模型添加到场景并自动飞行定位到模型位置

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Promise.&lt;void&gt;</code> - 无返回值，通过异步方式完成模型加载  
**Throws**:

- <code>Error</code> 当传入的 url 不符合要求（为空或无效）时抛出错误

| Param     | Type                                                   | Default         | Description                                                                                                                    |
| --------- | ------------------------------------------------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| url       | <code>string</code>                                    |                 | 3D Tiles 模型的 URL 地址，必填参数                                                                                             |
| [options] | <code>Cesium.Cesium3DTileset.ConstructorOptions</code> | <code>{}</code> | 3D Tiles 加载配置项， 参考 Cesium 官方文档：https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTileset.html#.ConstructorOptions |

<a name="MapCore+flyTo"></a>

### mapCore.flyTo(options)

将三维球相机飞行定位到指定的经纬度位置和高度，并设置相机姿态（有动画效果）

**Kind**: instance method of [<code>MapCore</code>](#MapCore)

| Param               | Type                  | Default           | Description                                           |
| ------------------- | --------------------- | ----------------- | ----------------------------------------------------- |
| options             | <code>Object</code>   |                   | 定位参数配置对象                                      |
| [options.longitude] | <code>number</code>   | <code>0</code>    | 目标位置的经度，单位：度                              |
| [options.latitude]  | <code>number</code>   | <code>0</code>    | 目标位置的纬度，单位：度                              |
| [options.height]    | <code>number</code>   | <code>2000</code> | 目标位置的高度，单位：米                              |
| [options.heading]   | <code>number</code>   | <code>348</code>  | 相机朝向（方位角），单位：度，0 表示正北，90 表示正东 |
| [options.pitch]     | <code>number</code>   | <code>-89</code>  | 相机俯仰角，单位：度，0 表示水平，正值向上，负值向下  |
| [options.roll]      | <code>number</code>   | <code>0</code>    | 相机翻滚角，单位：度，0 表示水平                      |
| [options.duration]  | <code>number</code>   | <code>0</code>    | 飞行持续时间，单位：秒，0 表示瞬间定位                |
| [options.cb]        | <code>function</code> | <code></code>     | 定位完成后的回调函数                                  |

**Example**

```js
// 示例1：定位到北京附近，使用默认参数
flyTo({
  longitude: 116.404,
  latitude: 39.915,
  height: 5000,
})
```

**Example**

```js
// 示例2：定位到上海，设置飞行时间3秒并添加回调
flyTo({
  longitude: 121.4737,
  latitude: 31.2304,
  height: 3000,
  heading: 0,
  pitch: -60,
  duration: 3,
  cb: () => {
    console.log('定位到上海完成')
  },
})
```

<a name="MapCore+setView"></a>

### mapCore.setView(options)

将三维球相机直接定位到指定的经纬度位置和高度，并设置相机姿态（无动画效果）

**Kind**: instance method of [<code>MapCore</code>](#MapCore)

| Param               | Type                | Default           | Description                                           |
| ------------------- | ------------------- | ----------------- | ----------------------------------------------------- |
| options             | <code>Object</code> |                   | 定位参数配置对象                                      |
| [options.longitude] | <code>number</code> | <code>0</code>    | 目标位置的经度，单位：度                              |
| [options.latitude]  | <code>number</code> | <code>0</code>    | 目标位置的纬度，单位：度                              |
| [options.height]    | <code>number</code> | <code>2000</code> | 目标位置的高度，单位：米                              |
| [options.heading]   | <code>number</code> | <code>348</code>  | 相机朝向（方位角），单位：度，0 表示正北，90 表示正东 |
| [options.pitch]     | <code>number</code> | <code>-89</code>  | 相机俯仰角，单位：度，0 表示水平，正值向上，负值向下  |
| [options.roll]      | <code>number</code> | <code>0</code>    | 相机翻滚角，单位：度，0 表示水平                      |

**Example**

```js
// 示例1：直接定位到广州，使用默认姿态
setView({
  longitude: 113.2644,
  latitude: 23.1291,
  height: 10000,
})
```

**Example**

```js
// 示例2：直接定位到成都，自定义相机姿态
setView({
  longitude: 104.0665,
  latitude: 30.5723,
  height: 8000,
  heading: 90, // 朝向东
  pitch: -45, // 向下倾斜45度
  roll: 0,
})
```

<a name="MapCore+zoomIn"></a>

### mapCore.zoomIn([rate])

放大三维地图视图

该函数通过让相机向前移动来实现地图放大效果，移动距离基于当前相机高度和放大倍率计算

**Kind**: instance method of [<code>MapCore</code>](#MapCore)

| Param  | Type                | Default          | Description                                           |
| ------ | ------------------- | ---------------- | ----------------------------------------------------- |
| [rate] | <code>number</code> | <code>5.0</code> | 放大倍率，数值越小放大程度越大，建议取值范围 1.1-10.0 |

**Example**

```js
// 使用默认倍率放大地图
zoomIn()
```

**Example**

```js
// 使用自定义倍率放大地图（放大程度更大）
zoomIn(2.0)
```

**Example**

```js
// 使用较小放大倍率（放大程度较小）
zoomIn(8.0)
```

<a name="MapCore+zoomOut"></a>

### mapCore.zoomOut([rate])

缩小三维地图视图

该函数通过让相机向后移动来实现地图缩小效果，移动距离基于当前相机高度和缩小倍率计算

**Kind**: instance method of [<code>MapCore</code>](#MapCore)

| Param  | Type                | Default          | Description                                           |
| ------ | ------------------- | ---------------- | ----------------------------------------------------- |
| [rate] | <code>number</code> | <code>5.0</code> | 缩小倍率，数值越小缩小程度越大，建议取值范围 1.1-10.0 |

**Example**

```js
// 使用默认倍率缩小地图
zoomOut()
```

**Example**

```js
// 使用自定义倍率缩小地图（缩小程度更大）
zoomOut(2.0)
```

**Example**

```js
// 使用较小缩小倍率（缩小程度较小）
zoomOut(8.0)
```

<a name="MapCore+getMapCenter"></a>

### mapCore.getMapCenter([car3]) ⇒ <code>Array</code>

获取指定点的经纬度和高度，默认获取地图中心点

该函数将笛卡尔坐标系位置转换为地理坐标系（经纬度），并对结果进行格式化处理
经度和纬度将转换为度并保留 7 位小数，高度将取整数

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Array</code> - 返回一个包含三个元素的数组，格式为 [经度, 纬度, 高度]

- 经度：数值类型，单位为度，保留 7 位小数
- 纬度：数值类型，单位为度，保留 7 位小数
- 高度：数值类型，单位为米，取整数

| Param  | Type                           | Description                                                                    |
| ------ | ------------------------------ | ------------------------------------------------------------------------------ |
| [car3] | <code>Cesium.Cartesian3</code> | 可选参数，指定的笛卡尔坐标系点。如果不提供，默认获取当前相机位置（地图中心点） |

**Example**

```js
// 获取当前地图中心点的经纬度和高度
const center = getMapCenter()
console.log(`中心点: 经度=${center[0]}, 纬度=${center[1]}, 高度=${center[2]}米`)
```

**Example**

```js
// 获取指定笛卡尔坐标点的经纬度和高度
const point = Cesium.Cartesian3.fromDegrees(116.404, 39.915, 500)
const coordinates = getMapCenter(point)
console.log(`指定点: 经度=${coordinates[0]}, 纬度=${coordinates[1]}, 高度=${coordinates[2]}米`)
```

<a name="MapCore+handleColor"></a>

### mapCore.handleColor([color]) ⇒ <code>Cesium.Color</code>

处理颜色值，支持将 rgba 格式转换为 Cesium 的 Color 对象。
如果输入颜色是 rgba 格式，会先将其转换为十六进制颜色值，再结合 alpha 值生成 Cesium.Color 对象。
如果输入颜色不是 rgba 格式，则直接通过 Cesium.Color.fromCssColorString 转换为 Cesium.Color 对象。

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Cesium.Color</code> - 返回 Cesium.Color 对象，表示处理后的颜色。  
**Note**: 1. 依赖 Cesium.Color.fromCssColorString 方法，用于将 CSS 颜色字符串转换为 Cesium.Color 对象。

| Param   | Type                | Default                          | Description                                                          |
| ------- | ------------------- | -------------------------------- | -------------------------------------------------------------------- |
| [color] | <code>string</code> | <code>&quot;#ffffff&quot;</code> | 输入的颜色值，可以是十六进制颜色（如 '#ffffff'）、RGB 或 RGBA 格式。 |

**Example**

```js
// 示例1：处理 RGBA 颜色
const result = handleColor('rgba(255, 255, 255, 0.5)')
console.log(result) // 输出 Cesium.Color 对象，alpha 值为 0.5

// 示例2：处理十六进制颜色
const result = handleColor('#ff0000')
console.log(result) // 输出 Cesium.Color 对象
```

<a name="MapCore+getLineMaterial"></a>

### mapCore.getLineMaterial(lineType, [opts]) ⇒ <code>Cesium.Material</code>

获取线条的材质
根据传入的线条类型和配置参数，返回对应的 Cesium 材质对象。
支持虚线、箭头线和普通线条材质的生成。

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Cesium.Material</code> - 返回对应的 Cesium 材质对象。

- 虚线：返回 `Cesium.PolylineDashMaterialProperty`。
- 箭头线：返回 `Cesium.PolylineArrowMaterialProperty`。
- 普通线条：返回 `Cesium.Color`。

| Param    | Type                | Description                                                                                                                                                              |
| -------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| lineType | <code>number</code> | 线条类型，来自 `MapMarkLineTypes` 枚举。 - `MapMarkLineTypes.dashed.id`：虚线 - `MapMarkLineTypes.arrow.id`：箭头线 - 其他值：普通线条                                   |
| [opts]   | <code>object</code> | 配置参数对象，默认为空对象。 - @property {string} [color] - 线条颜色，默认为#ff0000。 - @property {number} [dashLength] - 虚线的间隔长度，仅在 `lineType` 为虚线时有效。 |

**Example**

```js
const material = getLineMaterial(MapMarkLineTypes.dashed.id, { color: '#ff0000', dashLength: 16.0 })
console.log(material) // 输出 Cesium.PolylineDashMaterialProperty 对象
```

<a name="MapCore+addPoint"></a>

### mapCore.addPoint(options) ⇒ <code>Cesium.Entity</code>

在地图上添加一个点（Point），可以包含点、标签和图标（billboard）

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Cesium.Entity</code> - 返回添加到地图上的实体对象

| Param                  | Type                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------- | ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| options                | <code>object</code>            | 点的配置选项                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| options.longitude      | <code>number</code>            | 点的经度                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| options.latitude       | <code>number</code>            | 点的纬度                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| options.height         | <code>number</code>            | 点的高度                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| options.cartesian3Data | <code>Cesium.Cartesian3</code> | Cartesian3 对象                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| options.parent         | <code>number</code>            | 父对象                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| [options.id]           | <code>number</code>            | 点的唯一标识符，默认为 0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| [options.name]         | <code>string</code>            | 点的名称，默认为 '圆点'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [options.show]         | <code>boolean</code>           | 是否显示点，默认为 true                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [options.point]        | <code>object</code>            | 点的配置 - {number} [point.pixelSize=12] - 点的像素大小，默认为 12 - {string} [point.color='#ffffff'] - 点的颜色，默认为 '#ffffff' - {string} [point.outlineColor='#ff0000'] - 点轮廓的颜色，默认为 '#ff0000' - {number} [point.outlineWidth=2.0] - 点轮廓的宽度，默认为 2.0 - {Array<number>} [point.scaleByDistance=[3000, 1, 80000, 0.1]] - 根据距离缩放点的大小 - {number} heightReference - 高度参考，默认为 Cesium.HeightReference.CLAMP_TO_GROUND                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| [options.label]        | <code>object</code>            | 标签的配置 - {string} [label.text=''] - 标签文本，默认为空字符串 - {string} [label.fontSize='20px'] - 字体大小，默认为 '20px' - {number} [label.scale=1] - 标签缩放比例，默认为 1 - {boolean} [label.showBackground=false] - 是否显示背景，默认为 false - {string} [label.backgroundColor='rgba(0,0,0,0.8)'] - 背景颜色，默认为 'rgba(0,0,0,0.8)' - {Array<number>} [label.backgroundPadding=[7, 5]] - 背景填充，默认为 [7, 5] - {Cesium.HorizontalOrigin} [label.horizontalOrigin=Cesium.HorizontalOrigin.CENTER] - 水平对齐方式，默认为中心对齐 - {Cesium.VerticalOrigin} [label.verticalOrigin=Cesium.VerticalOrigin.CENTER] - 垂直对齐方式，默认为中心对齐 - {string} [label.fillColor='#ffffff'] - 文本颜色，默认为 '#ffffff' - {string} [label.outlineColor='#000000'] - 文本轮廓颜色，默认为 '#000000' - {number} [label.outlineWidth=1.0] - 文本轮廓宽度，默认为 1.0 - {Array<number>} [label.pixelOffset=[0, 0]] - 像素偏移，默认为 [0, 0] - {Array<number>} [label.scaleByDistance=[3000, 1, 80000, 0.1]] - 根据距离缩放标签的大小 - {number} heightReference - 高度参考，默认为 Cesium.HeightReference.CLAMP_TO_GROUND |
| [options.billboard]    | <code>object</code>            | 图标的配置 - {string} [billboard.image] - 图标图片路径 - {number} [billboard.width=34] - 图标宽度，默认为 34 - {number} [billboard.height=34] - 图标高度，默认为 34 - {number} [billboard.scale=1.0] - 图标缩放比例，默认为 1.0 - {Cesium.HorizontalOrigin} [billboard.horizontalOrigin=Cesium.HorizontalOrigin.CENTER] - 水平对齐方式，默认为中心对齐 - {Cesium.VerticalOrigin} [billboard.verticalOrigin=Cesium.VerticalOrigin.CENTER] - 垂直对齐方式，默认为中心对齐 - {Array<number>} [billboard.pixelOffset=[0, 4]] - 像素偏移，默认为 [0, 0] - {Array<number>} [billboard.scaleByDistance=[3000, 1, 80000, 0.1]] - 根据距离缩放图标的大小 - {number} billboard.rotation=0 - 旋转 - {number} heightReference - 高度参考，默认为 Cesium.HeightReference.CLAMP_TO_GROUND                                                                                                                                                                                                                                                                                                                                                       |

<a name="MapCore+addPolygon"></a>

### mapCore.addPolygon(pos, opts) ⇒ <code>Cesium.Entity</code>

在地图上添加多边形（Polygon）

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Cesium.Entity</code> - 返回添加到地图上的实体对象

| Param | Type                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pos   | <code>Array</code>  | 多边形顶点的位置数组，默认为 []，格式如：[{ longitude: 0, latitude: 0, height: 0 }]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| opts  | <code>object</code> | 多边形的配置选项，默认值如下： - {boolean} show - 是否显示多边形，默认为 true - {boolean} isCar3 - 是否使用 Cartesian3 坐标数据，默认为 false - {number} id - 多边形的唯一标识符，默认为 0 - {string} name - 多边形的名称，默认为空字符串 - {boolean} fill - 是否填充多边形，默认为 true - {string} color - 多边形的填充颜色，默认为 'rgba(255, 255, 255, 0.5)' - {boolean} outline - 是否显示多边形的轮廓，默认为 true - {string} outlineColor - 多边形轮廓的颜色，默认为 '#ff0000' - {number} outlineWidth - 多边形轮廓的宽度，默认为 3.0 - {number} classificationType - 分类类型，默认为 Cesium.ClassificationType.BOTH - {number} height - 多边形的高度，默认为 undefined - {number} heightReference - 高度参考，默认为 Cesium.HeightReference.NONE - {boolean} perPositionHeight - 是否支持 hierarchy 点的高度，默认为 false |

<a name="MapCore+remove"></a>

### mapCore.remove()

移除 entity

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
<a name="MapCore+removeById"></a>

### mapCore.removeById()

根据 id 移除 entity

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
<a name="MapCore+removeAll"></a>

### mapCore.removeAll()

移除所有 entity

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
<a name="MapCore+getById"></a>

### mapCore.getById(id) ⇒ <code>Cesium.Entity</code> \| <code>null</code>

根据 id 查找 entity

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Cesium.Entity</code> \| <code>null</code> - 返回 Cesium.Entity 对象或 null

| Param | Type                | Description  |
| ----- | ------------------- | ------------ |
| id    | <code>string</code> | entity 的 id |

<a name="MapCore+showEntityById"></a>

### mapCore.showEntityById(id, show)

根据 id 显示隐藏某个 entity

**Kind**: instance method of [<code>MapCore</code>](#MapCore)

| Param | Type                 | Default            | Description          |
| ----- | -------------------- | ------------------ | -------------------- |
| id    | <code>string</code>  |                    | entity 的 id         |
| show  | <code>boolean</code> | <code>false</code> | true=显示 false=隐藏 |

<a name="MapCore+zoomToEntityById"></a>

### mapCore.zoomToEntityById(id)

定位到 entity-没有动画效果

**Kind**: instance method of [<code>MapCore</code>](#MapCore)

| Param | Type                | Description  |
| ----- | ------------------- | ------------ |
| id    | <code>String</code> | entity 的 id |

<a name="MapCore+flyToEntityById"></a>

### mapCore.flyToEntityById(id)

飞到 entity-有动画效果

**Kind**: instance method of [<code>MapCore</code>](#MapCore)

| Param | Type                | Description  |
| ----- | ------------------- | ------------ |
| id    | <code>String</code> | entity 的 id |

<a name="MapCore+addPointSurveillance"></a>

### mapCore.addPointSurveillance([opts]) ⇒ <code>Cesium.Entity</code> \| <code>null</code>

在地图上添加监控摄像头标记点，可显示自定义图标和名称标签

该函数创建一个带有指定图标的监控标记点，并可选择性地添加名称标签。
标记点会被赋予特定 ID 格式以便于识别和管理。

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Cesium.Entity</code> \| <code>null</code> - 返回创建的地图实体对象，如果创建失败则返回 null  
**Throws**:

- <code>Error</code> 当缺少必需的 image 参数时，会抛出错误

| Param              | Type                | Default                                              | Description                            |
| ------------------ | ------------------- | ---------------------------------------------------- | -------------------------------------- |
| [opts]             | <code>Object</code> | <code>{}</code>                                      | 标记点配置选项对象                     |
| opts.id            | <code>string</code> |                                                      | 监控标记点的唯一标识符                 |
| [opts.name]        | <code>string</code> |                                                      | 监控标记点的名称，用于显示标签（可选） |
| opts.longitude     | <code>number</code> |                                                      | 标记点的经度，单位：度                 |
| opts.latitude      | <code>number</code> |                                                      | 标记点的纬度，单位：度                 |
| [opts.image]       | <code>string</code> | <code>&quot;&#x27;&#x27;&quot;</code>                | 标记点显示的图标图片路径（必需）       |
| [opts.imageWidth]  | <code>number</code> | <code>42</code>                                      | 图标宽度，单位：像素                   |
| [opts.imageHeight] | <code>number</code> | <code>35</code>                                      | 图标高度，单位：像素                   |
| [opts.textBgColor] | <code>string</code> | <code>&quot;&#x27;rgba(0,0,0,0.8)&#x27;&quot;</code> | 名称标签的背景颜色                     |
| [opts.fillColor]   | <code>string</code> | <code>&quot;&#x27;#ffffff&#x27;&quot;</code>         | 名称标签的文字颜色                     |

**Example**

```js
// 添加一个简单的监控标记点
const surveillancePoint = addPointSurveillance({
  id: 'camera001',
  longitude: 116.404,
  latitude: 39.915,
  image: '/images/camera-icon.png',
})
```

**Example**

```js
// 添加一个带名称标签的监控标记点
const labeledPoint = addPointSurveillance({
  id: 'camera002',
  name: '前门监控',
  longitude: 116.407,
  latitude: 39.916,
  image: '/images/camera-icon.png',
  imageWidth: 50,
  imageHeight: 40,
  textBgColor: 'rgba(255,0,0,0.7)',
  fillColor: '#ffffff',
})
```

<a name="MapCore+removePointSurveillance"></a>

### mapCore.removePointSurveillance(id)

移除地图上的单个监控标记点

该函数通过监控标记点的 ID，构建对应的实体 ID，然后从地图中移除该标记点实体
实体 ID 的构建规则与添加监控标记点时保持一致，确保能准确匹配目标实体

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**See**: addPointSurveillance - 对应的添加监控标记点方法

| Param | Type                                       | Description                                              |
| ----- | ------------------------------------------ | -------------------------------------------------------- |
| id    | <code>string</code> \| <code>Number</code> | 监控标记点（摄像头）的唯一标识符，与添加时使用的 id 一致 |

**Example**

```js
// 移除ID为'camera001'的监控标记点
removePointSurveillance('camera001')
```

**Example**

```js
// 移除ID为10086的监控标记点（数字类型ID）
removePointSurveillance(10086)
```

<a name="MapCore+removePointSurveillanceAll"></a>

### mapCore.removePointSurveillanceAll()

移除地图上所有的监控标记点

该函数通过筛选所有 ID 以监控标记类型前缀开头的实体，
批量移除地图上所有的监控标记点，不影响其他类型的实体
筛选规则与监控标记点的 ID 命名规范保持一致

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**See**

- removePointSurveillance - 移除单个监控标记点的方法
- addPointSurveillance - 添加监控标记点的方法

**Example**

```js
// 移除地图上所有监控标记点
removePointSurveillanceAll()
```

<a name="MapCore+showPointSurveillance"></a>

### mapCore.showPointSurveillance(id, [show])

显示或隐藏地图上的单个监控标记点

该函数通过监控标记点的 ID，构建对应的实体 ID，然后控制该标记点实体的显示状态
实体 ID 的构建规则与添加监控标记点时保持一致，确保能准确匹配目标实体

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**See**

- addPointSurveillance - 添加监控标记点的方法
- removePointSurveillance - 移除单个监控标记点的方法

| Param  | Type                                       | Default            | Description                                                   |
| ------ | ------------------------------------------ | ------------------ | ------------------------------------------------------------- |
| id     | <code>string</code> \| <code>Number</code> |                    | 监控标记点（摄像头）的唯一标识符，与添加时使用的 id 一致      |
| [show] | <code>Boolean</code>                       | <code>false</code> | 是否显示标记点，true 表示显示，false 表示隐藏，默认值为 false |

**Example**

```js
// 显示ID为'camera001'的监控标记点
showPointSurveillance('camera001', true)
```

**Example**

```js
// 隐藏ID为10086的监控标记点（使用默认值）
showPointSurveillance(10086)
```

<a name="MapCore+showPointSurveillanceAll"></a>

### mapCore.showPointSurveillanceAll([show])

显示或隐藏地图上所有的监控标记点

该函数通过筛选所有 ID 以监控标记类型前缀开头的实体，
批量控制所有监控标记点的显示状态，不影响其他类型的实体
筛选规则与监控标记点的 ID 命名规范保持一致

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**See**

- showPointSurveillance - 显示/隐藏单个监控标记点的方法
- addPointSurveillance - 添加监控标记点的方法

| Param  | Type                 | Default            | Description                                                           |
| ------ | -------------------- | ------------------ | --------------------------------------------------------------------- |
| [show] | <code>Boolean</code> | <code>false</code> | 是否显示标记点，true 表示显示所有，false 表示隐藏所有，默认值为 false |

**Example**

```js
// 显示地图上所有的监控标记点
showPointSurveillanceAll(true)
```

**Example**

```js
// 隐藏地图上所有的监控标记点（使用默认值）
showPointSurveillanceAll()
```

<a name="MapCore+addPolygonHouse"></a>

### mapCore.addPolygonHouse([opts]) ⇒ <code>Cesium.Entity</code> \| <code>null</code>

添加房屋的面状标记到地图上

该函数解析房屋的 geo 数据，创建多边形面状标记，并添加到地图中。
面状标记的 ID 采用特定格式，便于后续管理和操作。

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**Returns**: <code>Cesium.Entity</code> \| <code>null</code> - 返回创建的面状标记实体对象，若创建失败则返回 null  
**See**

- removePolygonHouse - 移除单个房屋面状标记的方法
- showPolygonHouse - 显示/隐藏单个房屋面状标记的方法

| Param        | Type                | Default         | Description                          |
| ------------ | ------------------- | --------------- | ------------------------------------ |
| [opts]       | <code>Object</code> | <code>{}</code> | 房屋面状标记的配置选项               |
| opts.id      | <code>Number</code> |                 | 房屋的唯一标识符                     |
| opts.geoData | <code>String</code> |                 | 房屋的地理数据，应为 JSON 字符串格式 |

**Example**

```js
// 添加一个房屋面状标记
const houseGeoData = '{"geometry":{"coordinates":[[[116.404,39.915],[116.405,39.915],[116.405,39.916],[116.404,39.916]]]},"properties":{"color":"rgba(255,255,0,0.5)"}}'
const houseEntity = addPolygonHouse({
  id: 1001,
  geoData: houseGeoData,
})
```

<a name="MapCore+removePolygonHouse"></a>

### mapCore.removePolygonHouse(id)

移除地图上的单个房屋面状标记

该函数通过房屋 ID 构建对应的实体 ID，从地图中移除指定的房屋面状标记
实体 ID 的构建规则与添加房屋面状标记时保持一致

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**See**

- addPolygonHouse - 添加房屋面状标记的方法
- removePolygonHouseAll - 移除所有房屋面状标记的方法

| Param | Type                | Description                              |
| ----- | ------------------- | ---------------------------------------- |
| id    | <code>Number</code> | 房屋的唯一标识符，与添加时使用的 id 一致 |

**Example**

```js
// 移除ID为1001的房屋面状标记
removePolygonHouse(1001)
```

<a name="MapCore+removePolygonHouseAll"></a>

### mapCore.removePolygonHouseAll()

移除地图上所有的房屋面状标记

该函数筛选所有 ID 以房屋标记类型前缀开头的实体，批量移除所有房屋面状标记
筛选规则与房屋面状标记的 ID 命名规范保持一致，不影响其他类型实体

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**See**

- removePolygonHouse - 移除单个房屋面状标记的方法
- addPolygonHouse - 添加房屋面状标记的方法

**Example**

```js
// 移除地图上所有房屋面状标记
removePolygonHouseAll()
```

<a name="MapCore+showPolygonHouse"></a>

### mapCore.showPolygonHouse(id, [show])

显示或隐藏地图上的单个房屋面状标记

该函数通过房屋 ID 构建对应的实体 ID，控制指定房屋面状标记的显示状态
实体 ID 的构建规则与添加房屋面状标记时保持一致

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**See**

- addPolygonHouse - 添加房屋面状标记的方法
- showPolygonHouseAll - 显示/隐藏所有房屋面状标记的方法

| Param  | Type                 | Default            | Description                                                 |
| ------ | -------------------- | ------------------ | ----------------------------------------------------------- |
| id     | <code>Number</code>  |                    | 房屋的唯一标识符，与添加时使用的 id 一致                    |
| [show] | <code>Boolean</code> | <code>false</code> | 是否显示标记，true 表示显示，false 表示隐藏，默认值为 false |

**Example**

```js
// 显示ID为1001的房屋面状标记
showPolygonHouse(1001, true)
```

**Example**

```js
// 隐藏ID为1001的房屋面状标记（使用默认值）
showPolygonHouse(1001)
```

<a name="MapCore+showPolygonHouseAll"></a>

### mapCore.showPolygonHouseAll([show])

显示或隐藏地图上所有的房屋面状标记

该函数筛选所有 ID 以房屋标记类型前缀开头的实体，批量控制所有房屋面状标记的显示状态
筛选规则与房屋面状标记的 ID 命名规范保持一致，不影响其他类型实体

**Kind**: instance method of [<code>MapCore</code>](#MapCore)  
**See**

- showPolygonHouse - 显示/隐藏单个房屋面状标记的方法
- addPolygonHouse - 添加房屋面状标记的方法
- showEntityById - 底层用于控制实体显示状态的方法

| Param  | Type                 | Default            | Description                                                         |
| ------ | -------------------- | ------------------ | ------------------------------------------------------------------- |
| [show] | <code>Boolean</code> | <code>false</code> | 是否显示标记，true 表示显示所有，false 表示隐藏所有，默认值为 false |

**Example**

```js
// 显示地图上所有的房屋面状标记
showPolygonHouseAll(true)
```

**Example**

```js
// 隐藏地图上所有的房屋面状标记（使用默认值）
showPolygonHouseAll()
```

<a name="VgoGis3dSDK"></a>

## VgoGis3dSDK : <code>object</code>

SDK 命名空间

**Kind**: global namespace  
<a name="MapTypes"></a>

## MapTypes : <code>enum</code>

天地图影像类型常量

**Kind**: global enum  
**Read only**: true  
**Properties**

| Name       | Type                | Default                             |
| ---------- | ------------------- | ----------------------------------- |
| SATELLITE  | <code>string</code> | <code>&quot;satellite&quot;</code>  |
| ELECTRONIC | <code>string</code> | <code>&quot;electronic&quot;</code> |

<a name="MarkerTypes"></a>

## MarkerTypes : <code>enum</code>

地图自定义图层类型常量

**Kind**: global enum  
**Read only**: true  
**Properties**

| Name         | Type                | Default                               |
| ------------ | ------------------- | ------------------------------------- |
| SURVEILLANCE | <code>string</code> | <code>&quot;surveillance&quot;</code> |
| HOUSE        | <code>string</code> | <code>&quot;house&quot;</code>        |

<a name="MapMarkLineTypes"></a>

## MapMarkLineTypes : <code>enum</code>

地图标注线类型常量

**Kind**: global enum  
**Read only**: true  
**Properties**

| Name   | Type                | Default                                                           |
| ------ | ------------------- | ----------------------------------------------------------------- |
| arrow  | <code>Object</code> | <code>{&quot;id&quot;:1,&quot;name&quot;:&quot;箭头&quot;}</code> |
| solid  | <code>Object</code> | <code>{&quot;id&quot;:2,&quot;name&quot;:&quot;实线&quot;}</code> |
| dashed | <code>Object</code> | <code>{&quot;id&quot;:3,&quot;name&quot;:&quot;虚线&quot;}</code> |
