jquery.utable.js 说明文档
{| class="wikitable"
|日期
|修改人
|版本
|说明
|-
|2017-5-8
|苏国潮
|0.1
|创建文档
|-
|2017-7-1
|苏国潮
|1.0
|完成文档
|-
| 
| 
| 
| 
|-
| 
| 
| 
| 
|}   

== 1目的 ==
此文档包含了用jquery.utable.js创建业务表格的所有知识。

== 2说明 ==
    本插件提供了列固定的功能，以及可按一系列自定义展示的配置

== 3起步 ==

=== 3.1创建一個容器 ===
    引入依赖文件后，在需要创建表格的地方编写个div标签作为容器，再编写初始化控件的代码即可呈现表格。

例如：

<nowiki><div id="utable1"></div></nowiki>

=== 3.2准备数据接口 ===
    创建一个data.json文件作为请求的数据接口，文件包含的有以下数据，其中TotalCount代表数据总数和，Items为要显示的数据序列，序列项必须保持属性、类型一致且具有唯一键代表数据项。
{| class="wikitable"
|{

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
|} 

=== 3.4载入utable ===
由于utable依赖jquery，所以首先引入jquery.js（>=1.8），再引入jquery.utable.js以及样式jquery.utable.css文件。
{| class="wikitable"
|<link  href="jquery.utable.css" rel="stylesheet"/>

<script  src="jquery.js"></script>

<script  src="jquery.utable.js"></script>
|}

=== 3.5初始化utable ===
{| class="wikitable"
|
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
|}

== 4详细说明 ==
=== 4.1配置说明 ===
==== 4.1.1.containerSelector  jquery容器选择器 ====
如：
$('''containerSelector''').utable(UTableOption) 
==== 4.2.2. UTableOption 表格主配置项 ====
如：
$(containerSelector).utable('''UTableOption''') 

属性说明： 
{| class="wikitable" style="width:100%"
|属性名
|类型
|说明
|默认值
|-
|condition
|Object
|过滤条件
| 
|-
|TableColumns
|Array('''UTableColumnOption''')
|列配置项数组
| 
|-
|Url
|String
|获取数据的地址
| 
|-
|TableClass
|String
|表格样式
|table  table-bordered
|-
|ShowCheckBox
|Boolean
|是否显示复选框
|false
|-
|ShowRadioBox
|Boolean
|是否显示单选框
|false
|-
|ShowRowIndex
|Boolean
|是否显示行索引
|false
|-
|ShowPager
|Boolean
|是否显示分页控件
|true
|-
|PageSize
|Number
|行页显示行数
|50
|-
|DefaultSortField
|String
|用于提供给后端排序的列名
|
 Id
|-
|DefaultSortWay
|<nowiki>String(asc|desc</nowiki>
|提供给后端排序时是正序还是倒序的依据
|asc
|-
|KeyField
|String
|数据项的主键
|Id
|-
|MemoryPage
|Boolean
|是否内存分页
| 
|-
|MemoryAllData
|Array
|当MemoryPage为true时，要进行内存分页的全部数据
| 
|-
|IndexColWidth
|Number
|索引列的宽度(px)
|50
|-
|CheckWidth
|Number
|复选框列的宽度
|30
|-
|TableBodyHeight
|Number
|表格内容高度
|200
|-
|FixedColumn
|Boolean
|是否启用固定列
|true
|-
|FootAlign
|String
|表格脚部的文本对齐方式
|Center
|-
|showNoData
|Boolean
|没有数据时是否显示showNoDataText
|true
|-
|showNoDataText
|String
|没数据时显示的文本
|
 暂无更多数据了
|-
|'''FooterOptions'''
|Object
|表脚的配置
|
|} 

回调事件和函数

1、rowClickHandler:void

说明：用户点击行事件
参数：    

evt 事件信息    

model 当前行数据项 

2、changeRadioButton:void    

说明：选择单选框时触发

    参数：

    evt事件信息

    model当前行数据项 

3、changeCheckboxButton:void

    说明：选择复选框时触发

    参数：

    evt事件信息

    model当前行数据项 

4、afterLoad:void

    说明：加载数据完成后触发

    参数：

    response 原始 response 对象 

    5、checkAllChangeHandler:void

        说明：选择全部回调方法

        参数：

            evt 事件信息

    6、beforePageChange:void

        说明：跳页前

        参数：            

evt 事件信息             

pageObj 跳页的参数信息                 

currentPageIndex：当前页码                 

pageSize：每页显示行数             

totalCount：总行数             

pageTotal：总页码  

7、parseItems: Array<Model>  

说明：本函数接收原始 response 对象，返回可以用于展示的数组
参数     

response    原始 response 对象         

返回    

            Array<Model> 展示的数组

==== 4.2.3.UTableColumnOption 配置项 ====
        UtableColumnOption代表表格列的配置项         

{| class="wikitable"
|属性
|说明
|-
|head:string
|列头文本
|-
|tag:string
|数据字段名
|-
|width:Number
|列宽度
|-
|sort:Number
|1为排序，0为不排序
|-
|sortTag
|排序的字段名
|-
|format:enum

{

string,money,rate,MoneySN,week,utc@日期格式

}
|显示类型
|-
|addClass:string
|额外列样式
|-
|Img:string
|图片链接
|-
|isLink:bool
|是否链接
|-
|url:string
|跳转地址
|-
|paras:string
|参数
|-
|Text:string
|显示文本
|-
|target:string
|链接目标(_blank,_self)
|-
|linkList:Array<'''LinkOption'''>
|按钮列表配置
|-
|align:string
|列表对齐方式，center，left，right
|-
|headAlign:string
|列头对齐方式,center,left,right
|-
|isOper:bool
|是否操作按钮
|-
|fixColumn:bool
|是否固定列
|-
|nowrap:bool
|是否换行
|-
|enums
|枚举对象定义，例子：

{

  Number: {

text: "数字", value: 20

}

}
|}
回调函数与事件：

1、 clickEvent 点击事件

a)  参数：evt 事件对象

  model 当前行的数据对象

rowTag 当前行的tr对象

2、 func：当没配置format时，每次展示数据时都会执行，执行后的返回值是改单元格显示的结果

参数：

        model 当前行对象

        text  文本

        cell  td Dom对象

link  a 标签对象

rowTag  tr 标签对象

==== 4.2.4. LinkOption配置项 ====
{| class="wikitable"
|属性
|说明
|-
|img
|图片路径
|-
|target
|点击的目标
|-
|url
|地址
|-
|paras
|参数
|-
|clickEvent
|点击事件
|-
|tip
|提示
|-
|text
|显示的文本
|-
|cssClass
| 
|}
回调函数与事件：

3、 clickEvent 点击事件

a)  参数：evt 事件对象

  model 当前行的数据对象

rowTag 当前行的tr对象 

4、 func：每次展示数据时都会执行，执行后的返回值是改单元格显示的结果

参数：

model 当前行对象

        text  文本

        cell  td Dom对象

link  a 标签对象

rowTag  tr 标签对象

==== 4.2.5 FooterOptions表脚配置项 ====
由于这里内容比较多，贴个示例代码： 

 Rows: [
                 {
                     RowType: "合计",
                     RowTypeNameIndex: 2,
                     Cells: [
                         {
                             CellIndex: 8,
                             // data 为请求回来的数据, cell为当前单元格Dom
                             Func: function (data, cell) {
                              //   console.log(data);
                                 var total=0;
                                 for(var i=0;i<data.Result.Items.length;i++){
                                     total+=data.Result.Items[i].money;
                                 }
                                 return total;
                             }
                         }
                     ]
                 },
                 {
                     RowType: "平均数",
                     RowTypeNameIndex: 2,
                     Cells: [
                         {
                             CellIndex: 8,
                             // data 为请求回来的数据, cell为当前单元格Dom
                             Func: function (data, cell) {
                                 var total=0;
                                 for(var i=0;i<data.Result.Items.length;i++){
                                     total+=data.Result.Items[i].money;
                                 }
                                 return total/data.Result.Items.length;
                             }
                         }
                     ]
                 }
             ] 
