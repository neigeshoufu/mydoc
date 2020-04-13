# **使用node.js操作mongodb**

### **1.需要的包**

- `mongoose`

### **2.使用**

#### **2.1连接数据库**

```javascript
const mongoose = require('mongoose')
//表结构
//const Schema = mongoose.Schema

//链接数据库
mongoose.connect('mongodb://localhost/wydx', { useNewUrlParser: true })
        .then(() => console.log('Connect success'))
        .catch(err => console.log(`Connect error:${err}`))
```

#### **2.2表结构**

- 可以不创建。但为了数据完整性约束建议创建

```javascript
//表结构
var schema2 = new Schema({
  test: {
    type: String, //数据类型
    required:true //必须填写
    lowercase: true // Always convert `test` to lowercase
  }
})
```

- 使用

```javascript
//将文档解构发布.返回模型构造函数
const User = mongoose.model('User', schema2)
```

- `User`是集合名

#### **2.3添加数据**

- 创建文档对象

```javascript
const user = new User({
    username:'Black',
    password:'234567'
})
```

- 插入文档对象到集合

```javascript
user.save()
    .then(ret => console.log(`Done!INSERT data ${ret}`))
    .catch(err => console.log(`ERROR:${err}`))
```

#### **2.5查询数据**

- `findOne`

```javascript
User.findOne({'username':'Daniel'}, 'username password')
    .then(users => console.log(`Found!${users}`))
    .catch(err => console.log(`ERROR:${err}`))
```

- `find`查询所有符合的数据。返回数据

```javascript
 User.find().then(users => console.log(`Found all${users}`)).catch(err => console.log(err))
```

#### **2.6更新数据**

```javascript
User.where({username:'Jack'}).updateMany({username:'Rose'})
    .then((ret) => console.log('Update success' + ret))
    .catch(err => console.log(`ERROR:${err}`))
```
- 还有update

#### **2.7删除数据**

```javascript
User.deleteMany({username:'Black'})
    .then(() => console.log(`DELETE DONE!`))
    .catch(err => console.log(`ERROR:${err}`))
```

### **3.更多操作查看文档**

- [mongoose](http://mongoosejs.net/docs/)

