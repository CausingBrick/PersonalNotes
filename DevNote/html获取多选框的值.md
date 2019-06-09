以下为使用JQuery获取input checkbox被选中的值代码:
```js
<html>
    <head>
        <meta charset="gbk">
        <!-- 引入JQuery -->
        <script src="jquery-1.3.1.js" type="text/javascript"></script>
    </head>

    <body>
        <input type="checkbox" value="橘子" name="check">橘子1</input>
        <input type="checkbox" value="香蕉" name="check">香蕉1</input>
        <input type="checkbox" value="西瓜" name="check">西瓜1</input>
        <input type="checkbox" value="芒果" name="check">芒果1</input>
        <input type="checkbox" value="葡萄" name="check">葡萄1</input>
        
        <input type="button" value="方法1" id="b1">
        <input type="button" value="方法2" id="b2">


    </body>
    
    <script>
        //方法1
        $("#b1").click(function(){
            //$('input:checkbox:checked') 等同于 $('input[type=checkbox]:checked')
            //意思是选择被选中的checkbox
            $.each($('input:checkbox:checked'),function(){
                window.alert("你选了："+
                    $('input[type=checkbox]:checked').length+"个，其中有："+$(this).val());
            });
        });
        
        //方法2
        $("#b2").click(function(){
            $.each($('input:checkbox'),function(){
                if(this.checked){
                    window.alert("你选了："+
                        $('input[type=checkbox]:checked').length+"个，其中有："+$(this).val());
                }
            });
        });
    </script>
</html>

Pasted from: <https://www.cnblogs.com/td960505/p/6123510.html>







开发时自己的代码为



<div class="col-md-6">

<form id="wechatList" role="form">

<legend>需同步微信公众号</legend>

<div class="form-group">

<!-- <label for="">label</label> -->

{{range $k,$v := .wechat}}

<input name="wechat" class="minimal" type="checkbox" value={{.Guid}} />{{.Name}}

{{end}}

</div>

</form>

</div>

<div class="col-md-6">

<form id="websiteList" role="form">

<legend>需同步的网站</legend>

<div class="form-group">

<!-- <label for="">label</label> -->

{{range $k,$v := .wechat}}

<input name="website" class="minimal" type="checkbox" value={{.Guid}} />{{.Name}}

{{end}}

</div>

</form>

</div>

</div>

<a id='opResultID' href='javascript:void(0);' style='display: none; margin-right: 10px; text-align: left; text-decoration: none; color: red;'></a>

<button id="btnOkSync" type="button" class="btn btn-success btn-flat">开始同步</button>

<button id="btnCancelSync" type="button" class="btn btn-warning btn-flat" data-dismiss="modal">取消</button>



$(document).ready(function () {

function submitData() {



// 获取微信列表生成字符串

var wehcatStrs = "";

$.each($('input[name="wechat"]:checked'), function () {

wehcatStrs += $(this).val()+",";

});



// 获取网站列表生成字符串

var websiteStrs = "";

$.each($('input[name="website"]:checked'), function () {

websiteStrs += $(this).val()+",";

});

console.log(websiteStrs)

};

// 同步

$('#btnOkSync').click(function () {

submitData();

});

});

//input[name="checkbox"]:checked

$('input[type="checkbox"].minimal, input[type="radio"].minimal').iCheck({

checkboxClass: 'icheckbox_minimal-blue',

radioClass: 'iradio_minimal-blue'

});
```