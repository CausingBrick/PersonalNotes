```html
<section class="content-header">
<h1>
发送短信或邮件
<small></small>
</h1>
<ol class="breadcrumb">
<li><i class="fa fa-dashboard"></i> 稿件处理中心</li>
<li class="active">约稿</li>
<li class="active">发送短信或邮件</li>
</ol>
</section>

<!-- Main content -->
<section class="content" style="padding-bottom:5px;">

<!-- Default box -->
<div class="box">
<div class="box-header with-border form-inline">
<button id="btnCancelAuthor" type="button" class="btnCopyrightBindCancel btn btn-warning btn-flat">返 回</button>
<a id='opResultID' href='javascript:void(0);' style='margin-right: 10px; text-align: left; text-decoration: none; color: red;'></a>
</div>
</div>
<!-- 表单 -->

<!-- /.box -->
<div class="box box-primary">
<div>
<div id="toolbar_right" class="box-header">
<h6 id="toolbar_btnList_left" class="box-title">
{{range $k, $v :=.toolbarOperations1}}
<button id="{{.component_id}}" class="{{.component_class}}">
{{i18n $.Lang .item_name}}
</button> {{end}}
</h6>
</div>
<!-- toolbar -->
<div id="toolbar_left" class="box-header form-inline">
<h6 id="toolbar_btnList_resource" class="box-title">
{{range $k, $v :=.toolbarOperations2}}
<button id="{{.component_id}}" class="{{.component_class}}">
{{i18n $.Lang .item_name}}
</button> {{end}}
</h6>
</div>
</div>

<!-- bootstrab table -->
<div class="row">

<div id="removePlan" class="col-md-6">
<table id="removeTable">
</table>
</div>

<div id="enterPlan" class="col-md-6 resourceDiv">
<table id="enterTable" class="enterTable">
</table>
</div>

</div>
</div>
</section>
<!-- /.content -->

<!--module js-->
<script type="text/javascript">
$(document).ready(function () {



function initReportRemove() {
$('#removeTable').bootstrapTable({
method: 'get',
cache: false,
height: $(window).height() - 255,
striped: true,
pagination: true,
sidePagination: "server", //服务端分页
queryParamsType: 'limit',
queryParams: queryParams, //参数
pageSize: 50,
pageNumber: 1,
pageList: [5000],
// search: true,
showColumns: true,
showRefresh: true,
toolbar: "#toolbar_left",
url: "/center/order/getAuthor",
columns: [{
checkbox: true,
disabled: false
}, {
field: "author_old_name",
title: "作者姓名",
align: "left",
valign: "middle",
sortable: "true"
}, {
field: "work_unit",
title: "工作单位",
align: "left",
valign: "middle",
sortable: "true"
}, {
field: "guid",
title: "操作",
visible: false
}],
});
}

initReportRemove();
initReportEnter();
$('#removeTable').on('load-success.bs.table', function (data) {
$('#enterTable').bootstrapTable('refresh')
});


function initReportEnter() {
$('#enterTable').bootstrapTable({
method: 'get',
cache: false,
height: $(window).height() - 255,
striped: true,
pagination: true,
sidePagination: "server", //服务端分页
queryParamsType: 'limit',
queryParams: queryParams, //参数
pageSize: 50,
pageNumber: 1,
pageList: [5000],
// search: true,
showColumns: true,
showRefresh: true,
toolbar: "#toolbar_right",
url: "/center/order/getAuthor",
columns: [{
checkbox: true,
formatter: function (value, row, index) {
//获得左表所有行数据的json对象
removeTableRows = $("#removeTable").bootstrapTable('getData');
// 根据row.列名 那状态确定返回 true/false
if (ifHasGUID(removeTableRows, row["guid"])) {
return {
disabled: true,
};
}
}
}, {
field: "author_old_name",
title: "作者姓名",
valign: "middle",
sortable: "true"
}, {
field: "author_pen_name",
title: "作者笔名",
valign: "middle",
sortable: "true"
}, {
field: "guid",
title: "操作",
visible: false
}],
});
}
//初始画面默认为档案
initReportEnter();
//进入作者列表
$(document).off("click", "#btnEnterAuthor").on("click", "#btnEnterAuthor", function () {
var guids = $.map($('#enterTable').bootstrapTable('getSelections'), function (row) {
return row.guid;
});
var data = $('#enterTable').bootstrapTable('getSelections');
Object.keys(data).forEach(function (key) {
data[key]["0"] = false;
});
$('#removeTable').bootstrapTable('append', data);

$('#enterTable').bootstrapTable('remove', {
field: 'guid',
values: guids
});
});

//移除作者列表
$(document).off("click", "#btnRemoveAuthor").on("click", "#btnRemoveAuthor", function () {
//获得右表的所有行数据
var enterTableData = $('#enterTable').bootstrapTable('getData');
//后台数据库需要获取的数据
var tablevalue = $("#removeTable").bootstrapTable('getSelections');
//左表待删除的数据
var waitDeleteOnLeftArr = new Array();
//右表待添加的数据
dataToRight = [];
if (tablevalue.length === 0)
return;
$.each(tablevalue, function (i, value) {
//该数据未出现在右表中，则加入右表
if (!ifHasGUID(enterTableData, value["guid"])) {
dataToRight.push({
guid: value["guid"],
author_old_name: value["author_old_name"],
author_pen_name: value["author_pen_name"]
});
}

waitDeleteOnLeftArr[i] = value["guid"];
});

//删除左表的数据
$("#removeTable").bootstrapTable('remove', {
field: 'guid',
values: waitDeleteOnLeftArr
});
//右表添加左表选中的数据的数据
$("#enterTable").bootstrapTable('prepend', dataToRight);
});
//发送短信和邮件
$(document).off("click", "#btnOrderSubmit").on("click", "#btnOrderSubmit", function () {
var tablevalue = $("#removeTable").bootstrapTable('getSelections');
if (tablevalue.length === 0)
return;
var strGUIDs = "";
$.each(tablevalue, function (i, value) {
strGUIDs += value["guid"] + ",";
});
strGUIDs = strGUIDs.substring(0, strGUIDs.length - 1);
//弹出对话框
$("#normalDialog").load("/center/order/orderSubmit?orderGUID={{.orderGUID}}&strGUIDs=" + strGUIDs, function () {
$("#normalModel").modal({
keyword: true
});
});
});

//服务端分页：请求服务数据时所传参数
function queryParams(params) {
$("#enterTable").bootstrapTable("removeAll");
return {
//每页多少条数据
pageSize: params.limit,
//偏移量
pageOffset: params.offset,
search: params.search,
}
}
$(window).resize(function () {
$('#removeTable').bootstrapTable('resetView');
$('#enterTable').bootstrapTable('resetView');
});



//module js
$(document).off("click", "#btnCancelAuthor").on("click", "#btnCancelAuthor", function (e) {
$("#op").hide();
$("#content").show();


});
});



// 判断json对象中是否含有指定guid
function ifHasGUID(jsonData, targetGUID) {
var flag = false;
if (jsonData.length == 0) {
return false;
}
$.each(jsonData, function (index, el) {
if (el.guid == targetGUID) {
flag = true;
return false; //跳除所有循环
}
});
return flag;
}

function length(obj) {
var count = 0;
for (var i in obj) {
count++;
}
return count;
};
</script>

```

