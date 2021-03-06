---
title: ð å¦ä½å¼å
linkTitle: å¦ä½å¼å
summary: An example of using Wowchemy's Book layout for publishing online courses.
date: '2021-01-24'
type: book
---



{{< toc hide_on="xl" >}}

## å¦ä½å¼å

- å©ç¨é¢å¶ç»ä»¶å®ç°éæ±ï¼åå°ä»£ç é
- ls
- IDE(é¼ æ ææ½/å±æ§éç½®)->json->é¡µé¢
- ç»ä»¶åºï¼ç¼è¾åº/é¢è§åºï¼å±æ§åº/äºä»¶åº
- ls

### å¨æ å¯è§åç¼ç¨

### ä½ä»£ç æ©å±è½å

#### ç»ä»¶

##### æ¸²æç®æ³

- test02ä¸­å­æ¾äºjsonæç®æ ·ä¾
- ç»ä»¶æ¸²ææ¶éå¯¹äºåæ éç¨æ·±åº¦ä¼åéåï¼ååºéåï¼åè·å®å­èç¹åè·æ ¹èç¹ï¼åéå±åä¸æ¸²æ

![Image text](https://raw.githubusercontent.com/design-thinking-czz/starter-hugo-online-course/main/content/course/training/image-20210720142736389.png)

- åæ¸²æ9å10ï¼ç¶åä½ä¸ºchildrenä¼ ç»8ï¼æ¸²æ8ï¼ç¶åæ¸²æ4ï¼ç¶å11ï¼ç¶åæ¸²æ8ï¼ç¶åæ¸²æ2

##### ç»ä»¶åç§°

- å è½½
- æ³¨å

```json
clas = require('../../common/${node.name}/${node.name}')
if (!clas) {
	throw new Error('ç»ä»¶%${node.path}ä¸å­å¨')
}
if(class.default) {
    clas = clas.default
}
Vue.component(clas.name, clas)
cache[node.path] = clas
```

- å±æ§æ¼è£

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



- åå»º

##### ç»ä»¶ç¼æ

- ç»ä»¶åè£:drop,drag,mask

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

ææ½ï¼ç¹å»æ¾ç¤ºå±æ§

##### ç»ä»¶å±æ§éç½®

- èªå®ä¹å±æ§ç»ä»¶å è½½
- ç»ä»¶å®ä¾propséå
- propsç±»åå¤æ­ï¼æ¾å°å¯¹åºçè¡¨åç»ä»¶
- ä»jsonæ¸²æåºè¡¨å
- è¡¨åå¼åæ´ï¼æ´æ°componentTree JSON
- éæ°æ¸²æ

##### è·¨ç»ä»¶äºä»¶äº¤äº

- å¨å±ç»ä»¶mixin
- çé¢åå»º å¨å±åé
- ç»ä»¶emitæ¹å
- å¨å±åéæ¹å
- å±æ§æ¼è£å°ææç»ä»¶

##### ç»ä»¶æ©å±

- git
- npm
- lerna

###### å¨çº¿åç 

- å¨æç¼è¯
- (ä¿å­ææä»¶ï¼åå¨æç¼è¯)

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



#### ä¸»é¢

#### æ¨¡ç

#### é»è¾

### å¨çå½å¨æç®¡ç

#### å¼å

#### æå»º

#### æµè¯

#### é¨ç½²

#### è¿ç»´

#### è¿è¥

## è®¾è®¡åå

- 1.ç»ä»¶å¯åµå¥
- ä¸è½æ¯ç®åç1+1=2,åºè¯¥æ¯1+1=æ ç©·
- 2.æè§å³æå¾
- å±æ§åæ­¥æ¾ç¤ºï¼éç½®æ°æ®å®æ¶æ¸²æ(ç¼è¾åºåå®æ½åºæ¸²æ)
- 3.ä½ä¾µå¥æ§
- ç»ä»¶ä¸è¦å³å¿ç¼è¾åè½çå·ä½å®ç°(ææ½ï¼è°æ´é¡ºåº);ç¼è¾åæ¾ç¤ºé½æ¯åä¸ä¸ªç»ä»¶ï¼å¯ä»¥ä¸å³å¿å±æ§çç¼è¾



## åå¸æµç¨

åå¸

åå¸ ------>ç»ä»¶æ·è´(æ ¹æ®jsonæ·è´å¼ç¨çæ¨¡åå°ç¼è¯æ¨¡çä¸­)------->ç¼è¯(npm run build)---------->ä¸ä¼ (éæèµæºæä»¶ä¸ä¼ cdn)---------->åæä»¶(åhtmlæä»¶å°ç£ç)

å¨æç¼è¯

æé(éå|æ¶æ¯éåBuil)------>ç¼è¯ç¯å¢åå¤(shellè°ç¨|Node forkå­è¿ç¨)------>ç¼è¯(æ¥å¿åä¼ |SSE WebSocket)
