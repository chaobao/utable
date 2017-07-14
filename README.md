
#1目的
此文档包含了用jquery.utable.js创建业务表格的所有知识。
#2说明
本插件提供了列固定的功能，以及可按一系列自定义展示的配置
#3起步
##3.1创建一個容器
引入依赖文件后，在需要创建表格的地方编写个div标签作为容器，再编写初始化控件的代码即可呈现表格。
例如：
<pre>
&lt;div id="utable1"&gt;&lt;/div&gt;
</pre>
##3.2准备数据接口
创建一个data.json文件作为请求的数据接口，文件包含的有以下数据，其中TotalCount代表数据总数和，Items为要显示的数据序列，序列项必须保持属性、类型一致且具有唯一键代表数据项。
<pre>
{
    "TotalCount": 500,
    "Items": [
      {
        "Id": 17644,
        "Content": "公告",
        "Title": "发布了新公告！",
        "MessageId": "6b848943a802488c80372a1f187ca61c",
      },
      {
        "Id": 17645,
        "Content": "公告",
        "Title": "发布了新公告！2",
        "MessageId": "6b848943a802488c80372a1f187ca61c"
      }
    ]
  }

</pre>
##3.4载入utable
由于utable依赖jquery，所以首先引入jquery.js（>=1.8），再引入jquery.utable.js以及样式jquery.utable.css文件。
<pre>
&lt;link href="jquery.utable.css" rel="stylesheet"/&gt;
&lt;script src="jquery.js"&gt;&lt;/script&gt;
&lt;script src="jquery.utable.js"&gt;&lt;/script&gt;
</pre>

##3.5初始化utable
```
<pre>

$("#utable1").uTable({
    Url: 'data.json',
    parseItems: function (response) {
        return response.Result.Items;
    },
    parseTotalCount: function (response) {
        return response.Result.TotalCount;
    },
    TableColumns: [
        {
            head: "内容", tag: " Content "
        }],
    TableClass: 'table table-bordered',
    PageSize: 5,
    DefaultSortField: 'Id',
    DefaultSortWay: 'Desc',
    KeyField: 'Id',
});
</pre>
```

#4详细说明
##4.1配置说明 
###4.1.1.containerSelector    jquery容器选择器
如：
$(containerSelector).utable(UTableOption)

###4.2.2. UTableOption 表格主配置项
如：
`$(containerSelector).utable(UTableOption)`

<table>
    <tbody>
        <tr class="firstRow">
            <td width="132" valign="top" style="border-width: 1px; border-color: windowtext; padding: 0px 7px;">
                <p>
                    属性名
                </p>
            </td>
            <td width="123" valign="top" style="border-top-width: 1px; border-right-width: 1px; border-bottom-width: 1px; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0px 7px;">
                <p>
                    类型
                </p>
            </td>
            <td width="100" valign="top" style="border-top-width: 1px; border-right-width: 1px; border-bottom-width: 1px; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0px 7px;">
                <p>
                    说明
                </p>
            </td>
            <td width="132" valign="top" style="border-top-width: 1px; border-right-width: 1px; border-bottom-width: 1px; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0px 7px;">
                <p>
                    默认值
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    condition
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Object
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    过滤条件
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;"></td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    TableColumns
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px; word-break: break-all;">
                <p>
                    Array(UTableColumnOption)
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    列配置项数组
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;"></td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    Url
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    String
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px; word-break: break-all;">
                <p>
                    获取数据的地址
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;"></td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    TableClass
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    String
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    表格样式
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    table &nbsp; table-bordered
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    ShowCheckBox
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Boolean
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    是否显示复选框
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    false
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    ShowRadioBox
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Boolean
                </p>
            </td>
            <td width="100" valign="top">
                <p>
                    是否显示单选框
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    false
                </p>
            </td>
        </tr>
        <tr>
            <td width="132">
                <p>
                    ShowRowIndex
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Boolean
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px; word-break: break-all;">
                <p>
                    是否显示行索引
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    false
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    ShowPager
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Boolean
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    是否显示分页控件
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    true
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    PageSize
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Number
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    行页显示行数
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    50
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    DefaultSortField
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    String
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    用于提供给后端排序的列名
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <pre>Id</pre>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    DefaultSortWay
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    String(asc|desc
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    提供给后端排序时是正序还是倒序的依据
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    asc
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    KeyField
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    String
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    数据项的主键
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Id
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    MemoryPage
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Boolean
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    是否内存分页
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;"></td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    MemoryAllData
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Array
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    当MemoryPage为true时，要进行内存分页的全部数据
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;"></td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    IndexColWidth
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Number
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    索引列的宽度(px)
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    50
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    CheckWidth
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Number
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    复选框列的宽度
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    30
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    TableBodyHeight
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Number
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    表格内容高度
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    200
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    FixedColumn
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Boolean
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    是否启用固定列
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    true
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    FootAlign
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    String
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    表格脚部的文本对齐方式
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Center
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    showNoData
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Boolean
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    没有数据时是否显示showNoDataText
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    true
                </p>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    showNoDataText
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    String
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    没数据时显示的文本
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <pre>暂无更多数据了</pre>
            </td>
        </tr>
        <tr>
            <td width="132" valign="top" style="border-right-width: 1px; border-bottom-width: 1px; border-left-width: 1px; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0px 7px;">
                <p>
                    FooterOptions
                </p>
            </td>
            <td width="123" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    Object
                </p>
            </td>
            <td width="100" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;">
                <p>
                    表脚的配置
                </p>
            </td>
            <td width="132" valign="top" style="border-top: none; border-left: none; border-bottom-width: 1px; border-bottom-color: windowtext; border-right-width: 1px; border-right-color: windowtext; padding: 0px 7px;"></td>
        </tr>
    </tbody>
</table>
