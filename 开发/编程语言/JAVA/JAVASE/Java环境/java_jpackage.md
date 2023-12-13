https://docs.oracle.com/en/java/javase/15/jpackage/index.html

# 15
## win
jpackage --dest packages --name BerylEnigma --app-version 1.3.3 --input .\jar\ --main-jar BerylEnigma.jar  --icon .\ico\BerylEnigma.ico --type app-image --description "BerylEnigma" --vendor "RyuZU, ffffffff0x" --copyright "Copyright 2020 ffffffff0x, MIT License"

# 16
## win
jpackage -n BE-BerylEnigma-win --app-version 1.6.1 -m "beryenigma/ffffffff0x.beryenigma.Main" --runtime-image .\beryenigma --dest ".\out\" --java-options "--add-opens java.base/java.lang.reflect=com.jfoenix" --icon .\ico\BerylEnigma.ico --type app-image --description "BerylEnigma" --vendor "RyuZU,ffffffff0x" --copyright "Copyright 2020 ffffffff0x,MIT License"

## linux
jpackage -n BE-BerylEnigma-linux --app-version 1.6.1 -m "beryenigma/ffffffff0x.beryenigma.Main" --runtime-image ./beryenigma --dest "./out/" --java-options "--add-opens java.base/java.lang.reflect=com.jfoenix" --icon ./ico/BerylEnigma.png --type app-image --description "BerylEnigma" --vendor "RyuZU,ffffffff0x" --copyright "Copyright 2020 ffffffff0x,MIT License"

## mac
jpackage -n BE-BerylEnigma-mac --app-version 1.6.1 -m "beryenigma/ffffffff0x.beryenigma.Main" --runtime-image ./beryenigma --dest "./out/" --java-options "--add-opens java.base/java.lang.reflect=com.jfoenix" --icon ./ico/BerylEnigma.icns --description "BerylEnigma" --vendor "RyuZU,ffffffff0x" --copyright "Copyright 2020 ffffffff0x,MIT License"

## 16.0.2
## win
jpackage -n BE-BerylEnigma-win --app-version 1.7.0 -m "beryenigma/ffffffff0x.beryenigma.Main" --runtime-image .\beryenigma --dest ".\out\" --java-options "--add-opens java.base/java.lang.reflect=com.jfoenix --add-exports javafx.base/com.sun.javafx.event=com.jfoenix --add-exports javafx.graphics/com.sun.javafx.scene=com.jfoenix" --icon .\ico\BerylEnigma.ico --type app-image --description "BerylEnigma" --vendor "RyuZU,ffffffff0x" --copyright "Copyright 2021 ffffffff0x,MIT License"


## 17
## win
jpackage -n BE-BerylEnigma --app-version 1.11.0 -m "beryenigma/ffffffff0x.beryenigma.Main" --runtime-image .\beryenigma --dest ".\out\" --java-options "--add-opens=java.base/java.lang.reflect=com.jfoenix --add-exports=javafx.controls/com.sun.javafx.scene.control.behavior=com.jfoenix --add-exports=javafx.base/com.sun.javafx.binding=com.jfoenix --add-exports=javafx.base/com.sun.javafx.event=com.jfoenix --add-exports=javafx.graphics/com.sun.javafx.stage=com.jfoenix --add-exports=javafx.graphics/com.sun.javafx.scene=com.jfoenix --add-exports=javafx.controls/com.sun.javafx.scene.control.behavior=com.jfoenix --add-exports=javafx.controls/com.sun.javafx.scene.control=com.jfoenix" --icon .\ico\BerylEnigma.ico --type app-image --description "BerylEnigma" --vendor "RyuZU,ffffffff0x" --copyright "Copyright 2021 ffffffff0x,MIT License"

## linux
jpackage -n BE-BerylEnigma --app-version 1.11.0 -m "beryenigma/ffffffff0x.beryenigma.Main" --runtime-image ./beryenigma --dest "./out/" --java-options "--add-opens=java.base/java.lang.reflect=com.jfoenix --add-exports=javafx.controls/com.sun.javafx.scene.control.behavior=com.jfoenix --add-exports=javafx.base/com.sun.javafx.binding=com.jfoenix --add-exports=javafx.base/com.sun.javafx.event=com.jfoenix --add-exports=javafx.graphics/com.sun.javafx.stage=com.jfoenix --add-exports=javafx.graphics/com.sun.javafx.scene=com.jfoenix --add-exports=javafx.controls/com.sun.javafx.scene.control.behavior=com.jfoenix --add-exports=javafx.controls/com.sun.javafx.scene.control=com.jfoenix" --icon ./ico/BerylEnigma.png --type app-image --description "BerylEnigma" --vendor "RyuZU,ffffffff0x" --copyright "Copyright 2021 ffffffff0x,MIT License"






---

jpackage --dest packages --name BEdemo --app-version 2.0 --input .\ --main-jar BerylEnigma-1.0.0_RD.jar  --icon BE.ico --win-shortcut --win-dir-chooser --description "Demo application for testing functionality" --vendor "Small, Inc" --copyright "Copyright 2020, All rights reserved"

jpackage --dest packages --name BEdemo --app-version 1.2 --input .\jar\ --main-jar BerylEnigma.jar  --icon BE.ico --win-shortcut --win-dir-chooser --description "Demo application for testing functionality" --vendor "RyuZU, ffffffff0x" --copyright "Copyright 2020 ffffffff0x, MIT License"

--type app-image

jpackage --name "BE" -m BE.Test/ffffffff0x.beryenigma.Main --module-path .\mods\BE.jmod;.\mods\javafx.base.jmod;.\mods\javafx.controls.jmod;.\mods\javafx.fxml.jmod;.\mods\javafx.graphics.jmod;C:\Users\RyuZU\.m2\repository\org\apache\commons\commons-text\1.3\commons-text-1.3.jar --icon .\ico\BE.ico --java-options "--add-opens java.base/java.lang.reflect=com.jfoenix" --type app-image --vendor "RyuZU, ffffffff0x" --copyright "Copyright 2020 ffffffff0x, MIT License"

.\mods\javafx.base.jmod
.\mods\javafx.controls.jmod
.\mods\javafx.fxml.jmod
.\mods\javafx.graphics.jmod

C:\Users\RyuZU\.m2\repository\org\apache\commons\commons-text\1.3\commons-text-1.3.jar

jpackage --type app-image -n name -m moduleName/className --runtime-image appRuntimeImage

稳定版本

jpackage --name "Modular-installer" --module-path jar\BE_Test-1.0.jar;C:\Users\RyuZU\.m2\repository\com\jfoenix\jfoenix\9.0.10\jfoenix-9.0.10.jar;C:\Users\RyuZU\.m2\repository\commons-codec\commons-codec\1.10\commons-codec-1.10.jar;C:\Users\RyuZU\.m2\repository\org\apache\commons\commons-lang3\3.7\commons-lang3-3.7.jar;C:\Users\RyuZU\.m2\repository\org\apache\commons\commons-text\1.3\commons-text-1.3.jar;C:\Users\RyuZU\.m2\repository\org\openjfx\javafx-base\16\javafx-base-16-win.jar;C:\Users\RyuZU\.m2\repository\org\openjfx\javafx-controls\16\javafx-controls-16-win.jar;C:\Users\RyuZU\.m2\repository\org\openjfx\javafx-fxml\16\javafx-fxml-16-win.jar;C:\Users\RyuZU\.m2\repository\org\openjfx\javafx-graphics\16\javafx-graphics-16-win.jar -m BE/ffffffff0x.beryenigma.Main --java-options "--add-opens java.base/java.lang.reflect=com.jfoenix" --vendor raven --type app-image




C:\Users\RyuZU\.m2\repository\com\jfoenix\jfoenix\9.0.10\jfoenix-9.0.10.jar;C:\Users\RyuZU\.m2\repository\commons-codec\commons-codec\1.10\commons-codec-1.10.jar;C:\Users\RyuZU\.m2\repository\org\apache\commons\commons-lang3\3.7\commons-lang3-3.7.jar;C:\Users\RyuZU\.m2\repository\org\apache\commons\commons-text\1.3\commons-text-1.3.jar;C:\Users\RyuZU\.m2\repository\org\openjfx\javafx-base\16\javafx-base-16-win.jar;C:\Users\RyuZU\.m2\repository\org\openjfx\javafx-controls\16\javafx-controls-16-win.jar;C:\Users\RyuZU\.m2\repository\org\openjfx\javafx-fxml\16\javafx-fxml-16-win.jar;C:\Users\RyuZU\.m2\repository\org\openjfx\javafx-graphics\16\javafx-graphics-16-win.jar