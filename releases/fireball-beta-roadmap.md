---
author: nantas
title: "Fireball Beta Roadmap"
permalink: /blogs/releases/beta-roadmap
---

## Fireball 0.4 (2015.05)

### 完成并稳定 cocos2d-js 整合

从0.4版开始， 新建 Fireball 项目时将会可以选择 Cocos2D-JS 作为底层引擎，Pixi 引擎仍然能够选用，但不是作为首选。Cocos2D-JS 相关的资源制作和导入功能会在后面版本中持续添加和完善。

### 加入曲线动画编辑器和程序接口

我们会在这个版本加入下列接口和组件：

- Entity.animate
- Animation component
- Animation clip

### Animation Editor

以及能够展示和编辑 Animation Clip 的动画编辑器。（类似于 Unity 的 Animation 编辑窗口）包括新增曲线控制点，操作节点控制手柄，添加动画事件等功能。

## Fireball 0.5 (Beta公测版，2015.06)

### Particle  组件

Particle 组件是通过 Cocos2D-JS 的粒子系统实现的在场景中配置和播放粒子的功能组件。该组件实现了在 Inspector 里添加 sprite 资源、调整参数，并在 Scene View 和 Game View 中预览粒子效果的功能。

未来版本中会加入专门的 Particle Asset 和 Particle Editor。

### Prefab 预制物体

类似 Unity 的 Prefab 概念，用户可以将装载和配置好组件的 Entity 保存为 Prefab，然后在程序中动态实例化。相比于 Unity 的 Prefab，我们改进了以下功能：

- Hierarchy 中将只能看到 Prefab 的 root 节点，Prefab 包含的子物体默认不会显示在 Hierarchy 中。
- 点击 Prefab 属性中的`edit`按钮，会进入 Prefab 编辑模式。这个时候会正常显示 Prefab 下面的 Entity 结构，而场景中无关的 Entity 会变暗且不能编辑。编辑模式下可以像操作正常 Entity 一样任意修改 Prefab 下的结构和组件。
- Prefab 子节点组件里的属性旁边会加入`expose`按钮，点击就可以将该属性暴露到 Prefab root 节点上，方便用户在不进入编辑模式的情况下就可以修改某些常用属性。
- Prefab 子节点 Entity 可以设置为`anchor`模式，这样在 Hierarchy 中就会可以看到这个子节点，方便用户在子节点上挂载武器、特效等动态物件。

### TexurePacker 数据导入

TexturePacker 是目前手游开发行业中最流行的图集编辑工具，Fireball 将可以直接导入 TexturePacker 生成的图集数据，并在游戏中享受批量渲染带来的性能提升。

### Sliced Sprite 九宫格 Sprite

九宫格 Sprite 多用于 UI 制作，能够以一个尺寸很小的图片生成可自由缩放的面板或背景 Sprite。生成 Sliced Sprite 后通过 Inspector 就可以编辑九宫格切分的参数和看到预览效果。

## Fireball 0.6 (2015.07)

这个版本将会对 Fireball 进行一次重构和升级, 这其中包括:

### 将 Fireball 底层 UI 框架从 Polymer 0.5 升级到 Polymer 0.8. 

这次升级会带来编辑器 UI 响应速度的巨大提升，由于 [Polymer 0.8](https://www.polymer-project.org/0.8/) 更多的兼容主流浏览器, Fireball 的界面开发将将和主流 Web 开发接轨, 用户开发扩展不仅可以使用 Fireball UI 框架, 还可以使用目前主流 Web 框架如 jQuery, Semantic UI, Bootstrap 等前端库.

### 开放 Fireball Editor 扩展接口.

Fireball 团队通过 Fireball-Editor-Framework 扩展 Fireball. 开放 Editor-Framework 将让 Fireball 的开发者和 Fireball 开发团队处于同一个开发层去扩展 Fireball, 这也是 Fireball 引擎的主体核心, 一个可随意定制扩展的游戏引擎.

### 将 Fire-Core 和 Fire-Engine 整合为开源项目 Engine-Framework, 并可以让用户单独使用

Engine-Framework 是一套 Entity-Component 系统. 他提供了一个 Entity-Component 系统所必须的类和模块: Entity-Component (scene graph), 事件系统 (event system), Entity 动画层 (entity.animate), 序列化抽象 (serialization), 属性定义 (property attribute), 场景更新 (scene update) 等. Engine-Framework 并不提供渲染, 输入, 声音等传统游戏引擎的工作, 他仅通过一个定义好的 Runtime 抽象层去和传统引擎 (pixi, cocos2d-js, three.js 等)交互. 所以用户可以在不借助 Fireball Editor 的情况下, 单独使用 Engine Framework 并和自己喜欢的引擎或自己的引擎做整合. 

### 升级 Fireball AssetDatabase

我们将全面重写 Fireball 的 Asset Database, 采用新的 Async 导入导出流程. 新的 Asset Database 将允许用户注册自己的资源 Meta 和导入导出规则, 并可以被 CLI 所使用.


## 未来版本功能

### Cocos Runtime 支持

### 整合3D引擎

我们将会整合像three.js这样的 3D 引擎，并在编辑器中加入 3D 游戏开发必要的工具和功能。

### 动画状态机

可以控制 2D 骨骼动画之间的过度和融合的动画状态机编辑器和程序接口。

### 可视化编程

面向非程序员用户的可视化游戏逻辑编辑器。这个工具类似于虚幻引擎的 Kismet 或 Unity 下的 PlayMaker。用户可以创建和移动游戏逻辑模块并将他们连接在一起来实现复杂的游戏性逻辑。所有逻辑块在运行游戏之前都会被编译成正常的代码，以方便程序员进行定制和调试。
