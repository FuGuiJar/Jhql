# Jhql

## 1. 引用 jhql





```js
let data = {
    gitName: '',
    token: ''
};
let jhql =  new Jhql(data);
```
```js
let content = `[
    {
        "id": 4,
        "userId": 2,
        "price": 1.1,
        "title": "delectus aut autem",
        "completed": false
    },
    {
        "id": 4,
        "userId": 2,
        "price": 1.1,
        "title": "delectus aut autem",
        "completed": false
    }
]`;



/*
	show() 
	展示所有表
*/
jhql.show().then(data => {
    console.log(data)
});	


/*
      init()
         初始化项目
 */
jhql.init().then(data => {
    console.log(data)
});	


/*
	select(tabName,where)
	tabName  表名
	where 条件 匿名函数 (item)=> {return item === 1}
	attr 列名,[atrr1.attr2]
*/
jhql.select('me',null,['id','title']).then(res => {
    console.log(res);
});	

jhql.select('me',(item)=>{
    return item.id === 2 
},['userId','title','id']).then(res =>{
    console.log(res);
});	


/*
	insert(tabName,data)
		新增数据
		! 判断数据结构必须一致
		！分表机制
*/
jhql.insert('me',content).then(data => {
    console.log(data);
});	

/*
	update
	set {name: '1'}
	where 条件 匿名函数 (item)=> {return item === 1}
*/
jhql.update('me', {
    price: 0,
    title: '这是一条测试数据'
},(user)=> {
    return user.id === 4
}).then(data => {
    console.log(data);
});	



/*
	create(tabName,content,type,message) 
	创建表
	tabName 表名称 -必选参数
	content 文件内容 -可选参数，默认为 '[]'
	type 文件类型 -可选参数，默认为 .json
	message 提交表得描述 -可选参数，默认为表得创建时间
*/
jhql.create('i1')
    .then(res=> {
    console.log(res);
})

/*	
	delete(tabName,where)
	删除数据
	tabName  表名
	where 条件 匿名函数 (item)=> {return item === 1}
	return
		attr: delLength 删除了n条数据
*/
jhql.delete('me',(item)=> {
    return item.userId === 2
}).then(res => {
    console.log(res);
});

/*
	remote(tabName)
	删除表
*/
jhql.remote('i1').then(res=> {
    console.log(res);
});
```



