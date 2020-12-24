#  CSS选择器

|       选择器        |       例子       | 说明                                                         |
| :-----------------: | :--------------: | ------------------------------------------------------------ |
|       .class        |     .toolbar     | 选择所有class="toolbar"的元素                                |
|         #id         |     #firstid     | 选择所有id="firstid"的元素                                   |
|          *          |        *         | 选择所有元素                                                 |
|          A          |        p         | 选择所有p标签的元素                                          |
|         A,B         |      div,p       | 选择所有div和p标签的元素                                     |
|         A B         |      div p       | 选择div标签所有后代中是p标签的元素                           |
|         A>B         |      div>p       | 选择div节点后直接子节点中为p标签的元素                       |
|         A~B         |      div~p       | 选择与div同级的所有p标签元素                                 |
|         A+B         |      div+p       | 当第二个元素*紧跟在*第一个元素之后，并且两个元素都是属于同一个父`元素`的子元素，则第二个元素将被选中 |
|     ~~A\|\|B~~      |  ~~col\|\|td~~   | 【不兼容多数浏览器】                                         |
|     [attribute]     |     [target]     | 选择所有包含target属性的元素                                 |
|  [attribute=value]  | [target=_blank]  | 选择所有属性target值为_blank的元素                           |
| [attribute~=value]  | [target~=flower] | 选择所有属性target中以空格作为分隔的值的列表中包含flower的元素 |
| [attribute\|=value] |   [lang\|=en]    | 选择所有属性lang的值是以en-为前缀的元素                      |
| [attribute*=value]  |   [class*=abc]   | 选择所有属性class的值中包含abc的元素                         |
| [attribute$=value]  |   [class$=abc]   | 选择所有属性class的值以abc结尾的元素                         |
|  [attibute^=value]  |   [class^=abc]   | 选择所有属性class的值以abc开头的元素                         |
|   [attr*=VaLUe i]   |  [class*=Abc i]  | 选择所有属性class的值包含abc(忽略大小写)的元素               |



