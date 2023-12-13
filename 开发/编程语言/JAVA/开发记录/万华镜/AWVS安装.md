# windows
无任何问题

# linux
1. 给.sh文件赋予可执行权限
2. 运行

报错
```bash
Acunetix Installer Version: v_210503151, Copyright (c) Acunetix
------------------------------------------------------------

Checking os...
Checking for dependencies...
    - dependency libXdamage.so.1 not found on the system
    - dependency libgdk-3.so.0 not found on the system
    - dependency libcairo.so.2 not found on the system
    - dependency libpango-1.0.so.0 not found on the system
    - dependency libgbm.so.1 not found on the system
    - dependency libatk-bridge-2.0.so.0 not found on the system
    - dependency libxkbcommon.so.0 not found on the system
    - dependency libXext.so.6 not found on the system
    - dependency libxcb.so.1 not found on the system
    - dependency libXfixes.so.3 not found on the system
    - dependency libgdk_pixbuf-2.0.so.0 not found on the system
    - dependency libatk-1.0.so.0 not found on the system
    - dependency libatspi.so.0 not found on the system
    - dependency libX11.so.6 not found on the system
    - dependency libXcomposite.so.1 not found on the system
    - dependency libX11-xcb.so.1 not found on the system
    - dependency libXrandr.so.2 not found on the system
    - dependency libgtk-3.so.0 not found on the system
    - dependency libcups.so.2 not found on the system
Some dependencies are not found on the system. Aborting installation.
Aborting installation
```

解决方案
```bash
yum install libXrender  libXext libXcursor  libXfixes libXcomposite libXrandr libXdamage  libXtst libXi cups-libs dbus-glib libXrandr libXcursor libXinerama cairo cairo-gobject pango  libXScrnSaver libatk-bridge-2.0.so.0 gtk3 -y
```

