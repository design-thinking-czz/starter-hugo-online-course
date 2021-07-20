---
title: 📊 如何开发
linkTitle: 如何开发
summary: An example of using Wowchemy's Book layout for publishing online courses.
date: '2021-01-24'
type: book
---



{{< toc hide_on="xl" >}}

## 如何开发

- 利用预制组件实现需求，减少代码量
- ls
- IDE(鼠标拖拽/属性配置)->json->页面
- 组件区，编辑区/预览区，属性区/事件区
- ls

### 全栈可视化编程

### 低代码扩展能力

#### 组件

##### 渲染算法

- test02中存放了json最简样例
- 组件渲染时针对二叉树采用深度优先遍历（后序遍历，先跑完子节点再跑根节点）和逐层向上渲染

{{< figure src="featured.jpg" >}}

- 先渲染9和10，然后作为children传给8，渲染8，然后渲染4，然后11，然后渲染8，然后渲染2

##### 组件名称

- 加载
- 注册

```json
clas = require('../../common/${node.name}/${node.name}')
if (!clas) {
	throw new Error('组件%${node.path}不存在')
}
if(class.default) {
    clas = clas.default
}
Vue.component(clas.name, clas)
cache[node.path] = clas
```

- 属性拼装

```json
render(h) {
    //...tree traverse to get single node
    let newProps = Object.assign({},globalVals,node.props);
	let children = node.children.map((item) => {
        return item.vnode;
    });
return (
	<div class="wrapper">
	{h(
	node.name,
	{
    	attrs: { cid: node.cid },
		props: newProps,
    },
	children
	)}
	</div>
	);
},
```



- 创建

##### 组件编排

- 组件包装:drop,drag,mask

```
node.vnode={
	<div class={cn}>
		<div name = 'spaceItem' class='space-item' on-dragenter={this.dragEnter} on-dragleave={this.dragLeave} on-dragover={this.dragOver} on-drop={this.insert} path={node.path} data-cid={node.cid} />
		<div class = 'component-wrapper' on-click={this.showProperty} on-dragstart={this.dragStart} on-dragleave={this.dragLeave} on-dragenter={this.dragEnter} on-drop={this.drop} name={node.name} path={node.path} data-cid={node.cid} draggable='true' on-click={this.showProperty}>
		{h(node.name,{
		attrs:{'cid':node.cid},props:newProps
		},children)}
		{children.length === 0 ? <div class='componnet-mask' /> : ''}
		</div>
	</div>
}
```

拖拽，点击显示属性

##### 组件属性配置

- 自定义属性组件加载
- 组件实例props遍历
- props类型判断，找到对应的表单组件
- 从json渲染出表单
- 表单值变更，更新componentTree JSON
- 重新渲染

##### 跨组件事件交互

- 全局组件mixin
- 界面创建 全局变量
- 组件emit改变
- 全局变量改变
- 属性拼装到所有组件

##### 组件扩展

- git
- npm
- lerna

###### 在线写码

- 动态编译
- (保存成文件，再动态编译)

```
let config ={
	entry: {
	RitComponent: [source],
	},
	output: {
	path: distPath,
	filename:compo.name+'.j'
	publicPath: '',
	library: compo.name,
	libraryTarget: 'umd'
	},
```



```
webpack(config ,(err, stats) => {
	if (err|| stats.hasErrors()) {
		console.error(err);
	}
	console.log('compile success');
	res.json({
		error_no: 0,
		error_msg: '',
		result: {
		js: distFile
		}
	});
	});
}
```



```
api.compile().then((data)=>{
	let reqjs = window['require'];
	reqjs.config({
		paths: {
			compo: data.result.js
		}
	});
	reqjs(['compo'],(Compo)=>{
		Vue.component(Compo.name , Compo);
		this.components.push(Compo.name);
	});
});
```



#### 主题

#### 模版

#### 逻辑

### 全生命周期管理

#### 开发

#### 构建

#### 测试

#### 部署

#### 运维

#### 运营

## 设计原则

- 1.组件可嵌套
- 不能是简单的1+1=2,应该是1+1=无穷
- 2.所见即所得
- 属性同步显示，配置数据实时渲染(编辑区和实施区渲染)
- 3.低侵入性
- 组件不要关心编辑功能的具体实现(拖拽，调整顺序);编辑和显示都是同一个组件；可以不关心属性的编辑



## 发布流程

发布

发布 ------>组件拷贝(根据json拷贝引用的模块到编译模版中)------->编译(npm run build)---------->上传(静态资源文件上传cdn)---------->写文件(写html文件到磁盘)

动态编译

排队(队列|消息队列Buil)------>编译环境准备(shell调用|Node fork子进程)------>编译(日志回传|SSE WebSocket)
