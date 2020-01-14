### 10、layer开关switch
+ 有种选择是否条件的表单内容，本来做成下拉，但后面说不好看换成开关，刚好项目里的layer插件的api里有开关，就不去找其他了，具体代码：
```
<input class='standard_network' value='0' lay-filter='networkswitch' type='checkbox' name="standard_network" lay-skin="switch" lay-text="是|否">
```
+ 由于switch在插件里是checkbox类型，与uniform插件冲突了，于是就在页面完成时append进去，再调用form.render渲染
+ 但这个开关的难点是，input的开关的value只有一个，改变开关状态的值不变，而且官方没有给出如何用js控制修改开关的方法，找了很久终于找到解决方案：首先是开关切换时要修改值，需要在lay.use里监听开关的改变：
```
form.on('switch(networkswitch)', function(data){
    if(data.elem.checked){
        $(".standard_network").val('1');
    }else{
        $(".standard_network").val('0');
    }
});  
```
+ 其次是手动控制开关，这里要注意改变了开关的同时也要修改value:
```
$("input[name='standard_network']").prop("checked",false);
$("input[name='standard_network']").val("0");
layui.form.render("checkbox");
```
