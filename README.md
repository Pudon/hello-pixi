## pixi
#### 创建渲染器（renderer）
创建一个可以播放动画的区域，相当于(`canvas`).
```
var renderer = PIXI.autoDetectRenderer(512, 512);
document.body.appendChild(renderer.view);
```
> 除了`autoDetectRenderer`接口，还有 `CanvasRenderer` 和 `WebGLRenderer` 接口，`autoDetectRenderer` 可以根据客户端对 WebGL 的支持自动创建 `WebGL` 或 `Canvas renderer`。

#### 创建舞台(stage)
舞台相当于一个容器(`Container`),添加元素后由渲染器(`renderer`)渲染舞台。相当于一个顶级的容器。

在 `pixi.js` 中有个 `Container()` 类，这个类就是一个容器。
```
var stage = new PIXI.Container();

添加舞台之后可以由渲染器(renderer)渲染。
renderer.render(stage);
// 舞台(stage)搭建完成后渲染出来。。 *最后
```
#### 创建材质集
动画中最重要的元素是图片（材质），这一类特殊的图片对象在`pixi.js`中称为精灵（`sprite`）,通过控制`sprite`的大小，位置及一些其他的属性，可以达到动画的效果。

在`pixi`中有一个`sprite`类，可以根据外部的图片（材质）来创建一个可以在`pixi`中使用的`sprite`对象。

**有三种方式创建：**
* 从某个单独的图片创建
* 从整个材质图片创建，根据材质上不同的位置和大小截取某部分来创建`sprite`
* 从材质集中创建
> 材质集是一个`json`文件，定义了某个材质图片里面图片的位置和大小等等，这样做的好处是不用每次创建`sprite`都要定义位置和大小，另外一方面修改了材质图片的时候不用修改代码.

#### 根据材质集加载图片
在 `pixi` 中有一个 `loader` 类来管理图片的加载，并且在加载完成后调用回调函数处理。
```
PIXI.loader
    .add("images/treasureHunter.json")
    .load(setup);
```
> `treasureHunter.json` 是材质集的配置文件，`setup` 是在完成图片加载后调用的回调函数。`PIXI.loader` 在加载完成后可以通过 `PIXI.loader.resources` 来获取加载的图片。

#### 回调函数
在完成图片加载后，`PIXI.loader` 会自动调用 `setup` 函数来进行下一步的处理。我们先定义一个测试方法，看看是否跟预期一样。
```
function setup() {
    console.log("加载完成.");
}
// 测试可以的话就可以，删除setup里面的东西，然后完善舞台。
```
#### 创建场景(gameScene)
游戏一般要创建两个场景，一个是用来显示正常游戏画面(gameScene)，一个是用来显示游戏结果(gameOverScene)。
```
var gameScene;

function setup() {
    gameScene = new PIXI.Container();
}
```
在容器中要添加所有的材质并创建对应的`sprite`，如何添加?通过`PIXI.loader.resources` 可以访问加载的素材。
```
var gameScene;

function setup() {
    gameScene = new PIXI.Container();
}
```
> 注意：pixi请求需要服务器
### 大幅度