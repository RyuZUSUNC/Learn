在创建Combo Box时，你必须实例化ComboBox类并定义一个Observable List作为其选项，这个步骤与其它的UI控件相似，例如ChoiceBox、ListView和TableView。

```java
ObservableList<String> options = 
    FXCollections.observableArrayList(
        "Option 1",
        "Option 2",
        "Option 3"
    );
final ComboBox comboBox = new ComboBox(options);
```

创建ComboBox的另外一种可选方法是先通过一个空的构造方法来创建Combo Box，然后调用其setItems方法，样例代码为：comboBox.setItems(options);

可以在任何时候向选项列表中添加新值。

```java
comboBox.getItems().addAll(
    "Option 4",
    "Option 5",
    "Option 6"
);
```

ComboBox类提供了一些便于使用的属性和方法。你可以使用setValue方法来指定在Combo Box中被选定的选项。当你在一个ComboBox对象上调用setValue方法时，selectionModel属性的被选项会被设置为对应值，即使该值并不在Combo Box的选项列表中也会如此。如果选项列表中包括了对应值，则对应的选项将会被选中。

类似地，你可以通过调用getValue方法来获得被选中的选项值。当用户选择了一个选项时，selectionModel属性的被选项和value属性都会被更新为新值。

你也可以限定Combo Box的下拉选项列表中可以展示的选项数量。下面的代码行表示允许Combo Box控件展示3个选项：comboBox.setVisibleRowCount(3)。调用此方法后，下拉选项可见的数量将会被限制为3，并且会出现一个滚动条（如图16-3所示）。

尽管ComboBox类有一个泛型注解并且允许用户使用各种类型来填充其选项，但还是不要用Node（或者任何其子类）作为填充类型。因为在场景图（Scene Graph）的概念中约定了在应用场景中，一个Node对象只可以出现在一个位置，因此被选中的选项会从ComboBox的选项列表中移除。当被选择项发生改变时，之前被选择项将会回到选项列表中，而新的被选择项则会被移除。为了避免出现这种情况可以使用Cell Factory机制，对应的解决方案在API文档中进行了说明。Cell Factory机制在你需要改变ComboBox对象的初始行为和外观时是非常有用的。

