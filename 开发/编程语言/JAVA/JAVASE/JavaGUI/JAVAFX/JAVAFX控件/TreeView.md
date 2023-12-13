在每棵树中，层次结构中最高的对象称为“根”。根包含几个子项，也可以有多个子项。没有孩子的物品称为“叶子”。

可以通过使用类的相应构造函数TreeItem或通过调用setGraphic方法，在每个树项上附带一个图形图标。
建议的图标大小为16x16，但实际上，Node可以将任何对象设置为图标，并且它是完全交互式的。

For通过调用getChildren和add方法，将在循环中创建的所有树项添加到根项。
也可以使用addAll方法而不是add方法来一次包含所有先前创建的树项目。

```java
for (int i = 1; i < 6; i++) {
            TreeItem<String> item = new TreeItem<String> ("Message" + i);            
            rootItem.getChildren().add(item);
        }    
```

可以在TreeView创建新TreeView对象时在类的构造函数中指定树的根，也可以通过调用类的方法setRootTreeView进行设置。

```java
TreeItem<String> rootItem = new TreeItem<String> ("Inbox", rootIcon);

TreeView<String> tree = new TreeView<String> (rootItem);
```

在根项目上调用setExpanded方法定义树视图项目的初始外观。
默认情况下，所有TreeItem实例都是折叠的，如果需要，必须手动对其进行扩展。
将true值传递给setExpanded方法，以使根树项目在应用程序启动时看起来已展开。

