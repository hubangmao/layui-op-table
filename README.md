  
![LOGO](https://images.gitee.com/uploads/images/2020/0315/012812_0de54be0_734930.png "OPTable.png")  
  
  
####  **介绍** 

Layui Table 数据列数过多解决方案。  
初衷 体验过类似效果的UI很实用，着手在Layui上实现了一套。  

[演示站点](https://hbangmao.gitee.io/OPTable/index.html) 

[更新日志](https://gitee.com/Hbangmao/layui-op-table/releases)  
  
> 支持功能

- [x] 展开内容(水平|垂直)显示
- [x] 展开显示表格
- [x] 展开内容从网络加载显示
- [x] 展开内容自定义标签显示

> 联系方式 

- QQ技术群: `730991854`
- 作者QQ：1414430109

#### 兼容问题 
![兼容问题](https://images.gitee.com/uploads/images/2020/0315/013759_46c24bb2_734930.png "QQ截图20200315011447.png")

<!--
#### 打赏 
如果喜欢作者的组件, 可以请作者喝肥仔水 ^_^  
   
![输入图片说明](https://images.gitee.com/uploads/images/2020/0315/021540_bbed19b7_734930.png "ic-wx-pay.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0315/021820_92c76b92_734930.png "101525_207b41b2_734930.png")
-->

#### 快速上手 

```
 layui.config({
    base: '../opTable'
  }).extend({
    opTable: '/opTable'
  }).use(['opTable'], function () {
  var opTable = layui.opTable.render({
      elem: '#test'
      , id: '#test'
      , url: 'static/test.json'
      , toolbar: '#toolDemo'
      , cols: [[
        {field: 'id', title: 'ID', sort: true}
        , {field: 'username', title: '用户名', edit: true}
        , {field: 'classify', title: '职业'}
        , {field: 'city', title: '城市', edit: true}
        , {title: '操作', toolbar: '#barDemo', width: 150, align: "center"}
      ]]

      //  展开的列配置
      , openCols: [
        {field: 'sex', title: '性别'}
        , {field: 'logins', title: '登录名', edit: true}
        , {field: 'sign', title: '签名'}
        , {field: 'wealth', title: '财富'}
        , {field: 'experience', title: '经验值'}
        , {field: 'experience', title: '积分'}
        , {field: 'score', title: '分数', edit: true}
      ]
    });
    
 });
```
#### 效果预览
![效果预览1](https://images.gitee.com/uploads/images/2020/0717/105747_80b12b12_734930.png "QQ截图20200717105424.png") 


#### 可配置属性  
![可配置属性](https://images.gitee.com/uploads/images/2020/0628/141951_dc80f752_734930.png "可配置属性.png")
#### 全局方法
![全局方法](https://images.gitee.com/uploads/images/2020/0316/130239_0067a947_734930.png "全局方法.png") 
#### 回调方法
![回调方法](https://images.gitee.com/uploads/images/2020/0316/130301_0042a2e9_734930.png "回调方法.png")

###  示例
[示例站点](https://hbangmao.gitee.io/OPTable/index.html)


##### 展开显示表格

```
 layui.opTable.render({
      elem: '#test1'
      , id: '#test1'
      , url: 'static/test.json'
      , cols: [[
        {field: 'id', title: 'ID', sort: true}
        , {field: 'username', title: '用户名', edit: true}
        , {field: 'city', title: '城市', edit: true}
      ]],

     /**
       * 展开显示表格 参数支持layui所有参数
       * @param itemData 当前行数据
       * @returns 支持 layui table 的所有配置参数
       *
       * 说明子表的 lay-filter='filter' 值与ID参数相同(去掉 # .)
       */
      openTable: function (itemData) {

        return {
          // 由于同时支持展开多个表格 组装唯一的id
          elem: '#child' + itemData.LAY_INDEX
          , id: 'child' + itemData.LAY_INDEX
          , url: 'static/test.json'
          , page: true
          , where: {id: itemData.id}
          , cols: [[
            {field: 'id', title: 'ID'}
            , {field: 'username', title: '用户名'}
            , {field: 'logins', title: '登录名'}
            , {field: 'city', title: '城市'}
            , {field: 'classify', title: '职业'}
            , {field: 'wealth', title: '财产值'}
            , {field: 'experience', title: '人气值'}
            , {field: 'score', title: '分数'}
            , {title: '操作', toolbar: '#barDemo', width: 150}
          ]]
        }
      }

    });
```
##### 效果预览

![展开显示表格](https://images.gitee.com/uploads/images/2020/0315/014136_eb18a686_734930.png "demo-open-table.png")


##### 展开显示树形表格
 _[演示](https://hbangmao.gitee.io/OPTable/layui-op-table/demo/index.html?href=href-op-tree)_ 

```
  var opTable = layui.opTable.render({
      elem: '#test-tree'
      , id: '#test-tree'
      , url: 'static/test.json'
      , cols: [[
        {field: 'id', title: 'ID', sort: true}
        , {field: 'username', title: '用户名', edit: true}
        , {field: 'city', title: '城市', edit: true}
      ]]
      /**
       * 展开显示树形表格
       * @param itemData 当前行数据
       * @returns
       *
       * 说明子表的 lay-filter='filter' 值与ID参数相同(去掉 # .)
       */
      , openTable: function (itemData) {
        return {
          elem: '#child_1_' + itemData.LAY_INDEX
          , id: 'child_1_' + itemData.LAY_INDEX
          , url: 'static/test2.json'
          , page: true
          , cols: [[
            {field: 'id', title: 'ID', edit: true}
            , {field: 'username', title: '用户名'}
            , {field: 'logins', title: '登录名'}
          ]]
          , openTable: function (itemData) {
            return {
              elem: '#child_2_' + itemData.LAY_INDEX
              , id: 'child_2_' + itemData.LAY_INDEX
              , url: 'static/test2.json'
              , page: true
              , cols: [[
                {field: 'id', title: 'ID', edit: true}
                , {field: 'username', title: '用户名'}
                , {field: 'logins', title: '登录名'}
              ]]
              , openTable: function (itemData) {
                return {
                  elem: '#child_3_' + itemData.LAY_INDEX
                  , id: 'child_3_' + itemData.LAY_INDEX
                  , url: 'static/test2.json'
                  , openVisible: false
                  , cols: [[
                    {field: 'id', title: 'ID', edit: true}
                    , {field: 'username', title: '用户名'}
                    , {field: 'logins', title: '登录名'}
                    , {field: 'city', title: '城市'}
                    , {field: 'classify', title: '职业'}
                    , {field: 'wealth', title: '财产值'}
                    , {field: 'experience', title: '人气值'}
                    , {field: 'score', title: '分数'}
                    , {title: '操作', toolbar: '#barDemo', width: 150}
                  ]]
                  , done: function () {
                    //  监听子表 修改
                    layui.table.on('edit(' + 'child' + itemData.LAY_INDEX + ')', function (obj) {
                      layer.msg(JSON.stringify(obj.data, null, "\t"));
                    });
                  }
                  , onEdit: function (data) {
                    console.log("表格4修改", data)
                  }
                }
              }
            }
          }
        }
      }
      , openType: 1
      , onEdit: function (data) {
        console.log("表格1修改", data)
        layer.msg(JSON.stringify(data));
      }
    });
```
##### 效果预览  
![展开显示树形表格](https://images.gitee.com/uploads/images/2020/1024/110251_e300fa76_734930.png "展开显示树形表格")
##### 展开从网络加载内容

```
layui.opTable.render({
      elem: '#test2'
      , id: '#test2'
      , url: 'static/test.json'
      , cols: [[
        {field: 'id', title: 'ID', sort: true}
        , {field: 'username', title: '用户名', edit: true}
        , {field: 'city', title: '城市', edit: true}
      ]],

      //  展开的列从网络加载
      openNetwork: {
        openCols: [
          {field: 'sign', title: '签名'}
          , {field: 'wealth', title: '财富'}
          , {field: 'experience', title: '积分'}
          , {field: 'classify', title: '职业'}
        ],
        /**
         *
         * @param data 当前行数据
         * @param success 成功
         * @param message 显示异常消息[没有数据 出错 等]
         */
        onNetwork: function (data, success, message) {
          // 从网络加载
          layui.$.ajax({
            type: "get",
            url: "static/test1.json",
            dataType: "json",
            data: {id: data.id},
            async: true,
            success: function (resp) {
              if (resp.code === 200) {
                setTimeout(function () {
                  if (data.id === 10000) {
                    message("加载出错");
                  } else {
                    success(resp.data);
                  }
                }, 200);
              } else {
                message("没有数据");
              }
            },
            error: function (err) {
              message("加载出错");
            }
          });
        }
      });
```
##### 效果预览
![网络加载内容](https://images.gitee.com/uploads/images/2020/0315/014826_355e5d44_734930.png "demo-network.png")

### 拓展

##### 列描述


```
// 有时候我们需要对某一数据列新增说明，来提高使用者对该项数据的深入了解 。

...
 cols: [[
          {field: 'username', title: '用户名', opHelp: {text: '主要用于论坛中作为昵称展示。', tipOpt: {}}, edit: true}
      ]]
...


...
 openCols: [
        {field: 'sign', title: '签名', opHelp: {text: '设置属于你的签名吧 。', tipOpt: {}}}
      ]
...

```
##### 效果预览

![数据列描述](https://images.gitee.com/uploads/images/2020/1024/113553_b72461cd_734930.png "数据列描述.png")


### 关于作者


```
过程中出问题了先自己捋一捋 

hubangmao 90后, 热爱 User interaction( UI ) 的Java程序猿 。

做完了一件非常开心非常Nice的事情。

此项目长期维护，以码云更新为准，祝你使用愉快 。  

```



