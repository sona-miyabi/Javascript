### 运行: chrome
>   localforage 是一个可以简单操作localStorage, WebSQL, indexedDB 的模块
>  参考 https://github.com/localForage/localForage
>  参考 https://localforage.github.io/localForage/#multiple-instances-createinstance
>  [准备] 导入库文件地址
>  [localforage](https://cdnjs.cloudflare.com/ajax/libs/localforage/1.7.2/localforage.min.js)


### 连接数据库

> 连接自定义的数据库(同步)
> ```javascript
> let db = localforage.createInstance({
> 	name: "dbName",			// 数据库名称
> 	//storeName:'objectStoreName',	// 存储对象名称
> });
> ```

> 默认连接数据库
> ```javascript
> let db = localforage;	// { name:'localforage', storeName:'keyvalepairs' }
> ```

> 版本的自动升级(objectStore)
> ```javascript
> // 假设当前版本为2
> localforage.createInstance({name:1, storeName:1});// 此时版本将内部升级为3
> localforage.createInstance({name:1, storeName:2});// 此时版本将内部升级为4
> localforage.createInstance({name:1, storeName:3});// 此时版本将内部升级为5
> // 因为创建新的ObjectStore时,必须借助onupgradeneeded事件来实现, 这个需要升级版本
> 
> localforage.dropInstance({name:1, storeName:1});// 此时版本将内部升级为6
> localforage.dropInstance({name:1, storeName:2});// 此时版本将内部升级为7
> // 问题: 有时执行删除, 却不会被删除. 且之后的读写操作都将返回 {Promise <pending>}
> ```

### 配置 db.config(opt)
>  提示: 对于indexedDB, 真正常用的就只有 name 和 storeName

> 设置配置
> ```javascript
> let opt={
> 	driver:[localforage.INDEXEDDB, localforage.WEBSQL, localforage.LOCALSTORAG],// 首选驱动顺序, 与setDriver上面传递的格式相同
> 	name:'localforage',	// 数据库的名称, 在localStorage中用于键的前缀
> 	size:4980736,		// 数据库字节大小, 仅用于WebSQL
> 	storeName:'keyvaluepairs',	// 数据存储的名称, IndexedDB中的objectStore名; WebSQL中的表名. (任何非字母数字字符都将转换为下划线)
> 	version:1.0,	// 数据库的版本, 仅用于WebSQL和IndexedDB, 在WebSQL中只是设置版本, 在IndexedDB中当触发onupgradeneeded事件时被调用.
> 	description:''	// 数据库的描述，基本上针对开发者的使用。
> }
> localforage.config(opt)

> 读取配置
> ```Javascript
> localforage.config();		// {name, storeName, ...}
> localforage.config('name');	// 获取name
> ```

### 数据操作
> 连接
> ```javascript
> let db=localforage.createInstance({ name:'1', storeName:'1' });
> ```

> 保存
> ```javascript
> db.setItem('k', 'v').then( v=>console.log(v) ).catch( err=>console.log(err) );	// 设置k键的值
> ```

###删除
```javascript
db.removeItem('k').then( ()=>{} ).catch( err=>console.log(err) );		// 删除k键的值
```

### 批量操作

* 清空数据库所有键的值 
```javascript
db.clear()
.then( ()=>{} )
.catch( err=>console.log(err) );
```

### 读取

> 获取索引的值 (未知键名, 用索引时)
> ```javascript
> db.key(0)
> .then( v=>console.log(v) )
> .catch( err=>console.log(err) );
> ```

> 获取键名的值(已知键名时)
> ```javascript
> db.getItem('k')
> .then( v=>console.log(v) )
> .catch( err=>console.log(err) );	// 
> ```

> 获取所有键名(数组)
> ```javascript
> db.keys()
> .then( v=>console.log(v) )
> .catch( err=>console.log(err) )
> ```

> 获取键值对数量
> ```javascript
> db.length()
> .then( v=>console.log(v) )
> .catch( err=>console.log(err) )
> ```



### 遍历
> ```javascript
> let collection=[];
> db.iterate( function (v,k,count){
> 	collection.push([k,v,count]);	// 将遍历结果插进去
> 	if(count>3) return '提前结束';	// 即便有更多的数据, 也可提前结束遍历, 反馈目前结果
> })
> .then(res=>console.log(res,collection))		// '提前结束'
> .catch(err=>console.log(err))
> ```
