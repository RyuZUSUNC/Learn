# Model
Let's start with the most basic concept here – the Model.

Simply put, the model can supply attributes used for rendering views.

To provide a view with usable data, we simply add this data to its Model object. Additionally, maps with attributes can be merged with Model instances:

简单来说，模型可以提供用于渲染视图的属性。

为了给视图提供可用的数据，我们只需将这些数据添加到其Model对象中即可。此外，带属性的映射可以与Model实例合并。
```java
@GetMapping("/showViewPage")
public String passParametersWithModel(Model model) {
    Map<String, String> map = new HashMap<>();
    map.put("spring", "mvc");
    model.addAttribute("message", "Baeldung");
    model.mergeAttributes(map);
    return "viewPage";
}
```

# ModelMap
Just like the Model interface above, ModelMap is also used to pass values to render a view.

The advantage of ModelMap is it gives us the ability to pass a collection of values and treat these values as if they were within a Map:

就像上面的Model接口一样，ModelMap也被用来传递值来渲染视图。

ModelMap的优点是它让我们能够传递一个值的集合，并把这些值当作Map中的值来处理。

```java
@GetMapping("/printViewPage")
public String passParametersWithModelMap(ModelMap map) {
    map.addAttribute("welcomeMessage", "welcome");
    map.addAttribute("message", "Baeldung");
    return "viewPage";
}
5. ModelAndVie
```

# ModelAndView
The final interface to pass values to a view is the ModelAndView.

This interface allows us to pass all the information required by Spring MVC in one return:

向视图传递值的最后一个接口是ModelAndView。

这个接口允许我们在一次返回中传递Spring MVC所需要的所有信息。

```java
@GetMapping("/goToViewPage")
public ModelAndView passParametersWithModelAndView() {
    ModelAndView modelAndView = new ModelAndView("viewPage");
    modelAndView.addObject("message", "Baeldung");
    return modelAndView;
}
```