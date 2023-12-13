# JavaFX窗口最大化及全屏相关设置
1. java8中可以一行做到窗口最大化
```java
stage.setMaximized(true);
```

2. 窗口始终显示在其他窗口之上
   
```java
stage.setAlwaysOnTop(true);
```

3. 窗口全屏，ESC退出

```java
stage.setFullScreen(true);
```

4. 最小化窗口，任务栏可见图标

```java
stage.setIconified(true);
```

5. 禁止窗口大小变化

```java
stage.setResizable(false);
```

6. 设置窗口风格

```java
stage.initStyle([StageStyle]);
```

StageStyle有几种类型
1) DECORATED——白色背景，带有最小化/最大化/关闭等有操作系统平台装饰（ 默认设置）

2) UNDECORATED——白色背景，没有操作系统平台装饰

3) TRANSPARENT——透明背景，没有操作系统平台装饰

4) UTILITY——白色背景，只有关闭操作系统平台装饰

5) UNIFIED——有操作系统平台装饰，消除装饰和内容之间的边框，内容背景和边框背景一致，（但要视平台支持），可以通过`javafx.application.Platform.isSupported(javafx.application.ConditionalFeature)`判断