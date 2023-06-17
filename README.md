# linkageview_pro
此库由fantasysea作者linkageview更新而来 原地址https://github.com/fantasysea/linkageview
更改目标
1、升级空安全
2、解决左侧商品分类栏外部调用setState导致的指示条位置异常，具体表现：右侧商品正常滚动时会判断是否为标题栏(是否需要切换下一个分类)从而更改左侧分类栏指示条位置和浮动指示条样式，正常情况下左右两方将同步协调更新我们不会发现有问题，但此组件我们将会嵌套使用不可避免的需要在外部更新从代码逻辑上来说作者做的没问题比较有意思的是这个变量"groups"作者将它放到下方代码段里
 ```
class LinkageView<T extends BaseItem> extends StatefulWidget {
    final List<T>? groups = [];//这其实没什么问题
    super(key: key){ //作者在这里对groups 进行初始化更新
     //简化版
         for (var i = 0; i < items.length; i++) {
      items[i]
        ..index = i
        ..isSelect = false;
      if (items[i].isHeader) {
        groups.add(items[i]);
      }
    }
    }
 ```
正常使用没问题，在组件内部调用setState也是没问题但在外部调用setState时会触发super而重新将groups初始化最终导致 分类栏指示条位置错误

