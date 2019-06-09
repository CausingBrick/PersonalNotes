# datetimepicker设置当期时间之前不可选方法

* 在datetimepicker构造函数里添加如下代码即可.

  >startDate:new Date(),

* 使用栗子:

    ```js
    //时间控件
    $('.deadlineTime').datetimepicker({
        format: 'yyyy-mm-dd hh:ii',
        language: 'zh-CN',
        startDate:new Date(),
    });
    ```

