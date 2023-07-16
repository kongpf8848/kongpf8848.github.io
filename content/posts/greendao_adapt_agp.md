---
title: "greenDAO适配AGP 8.0+版本🚀"
date: 2023-07-16
description: "本文介绍如何适配greenDAO以使用最新的Android Gradle Plugin 8.0+版本."
tags: ["greenDAO", "gradle", "android"]
type: post
---

[![scene.png](https://s1.ax1x.com/2023/07/16/pCIP7cQ.png)](https://imgse.com/i/pCIP7cQ)

# 前言

在做的一个[Kotlin](https://kotlinlang.org/)项目用到的数据库框架是[greenDAO](https://github.com/greenrobot/greenDAO)，在将项目升级到AGP 8.0版本后，编译时由于greenDAO版本不兼容导致编译不过，经过一番摸索，最终解决了greenDAO在AGP 8.0+版本下的编译报错问题，特此记录一下😄

# 环境

| 名称 | 版本 |
| :---: | :---: |
| Android Studio | `Flamingo，2022.2.1 Patch 2 `|
| JDK |  `17.0.6` |
| Gradle |  `8.0.2` |
| Android Gradle Plugin |  `8.0.2` |
| targetSdkVersion|  `33` |


# 升级greenDAO插件版本到3.3.1

修改项目根目录下的`build.gradle`文件，内容如下：

```groovy
buildscript {
    repositories {
        google()
        mavenCentral()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:8.0.2'
        classpath 'org.greenrobot:greendao-gradle-plugin:3.3.1'
    }
}
```

# 升级greenDAO依赖版本到3.3.0

修改项目模块如app模块下的`build.gradle`文件，内容如下：
```groovy
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-android-extensions'
    id 'kotlin-kapt'
    id 'org.greenrobot.greendao'
}

greendao {
    schemaVersion 19
    daoPackage 'xxx'
    targetGenDir 'src/main/java'
}

dependencies {
    implementation 'org.greenrobot:greendao:3.3.0'
}

```
然后编译，还是编译不过，报错内容如下：
```bash
org.gradle.internal.execution.WorkValidationException: Some problems were found with the configuration of task ':app:greendao' (type 'DefaultTask').
  - Gradle detected a problem with the following location: '/Users/kongpf/Desktop/mail-android/app/src/main/java'.
    
    Reason: Task ':app:compileOfficialDebugKotlin' uses this output of task ':app:greendao' without declaring an explicit or implicit dependency. This can lead to incorrect results being produced, depending on what order the tasks are executed.
    
    Possible solutions:
      1. Declare task ':app:greendao' as an input of ':app:compileOfficialDebugKotlin'.
      2. Declare an explicit dependency on ':app:greendao' from ':app:compileOfficialDebugKotlin' using Task#dependsOn.
      3. Declare an explicit dependency on ':app:greendao' from ':app:compileOfficialDebugKotlin' using Task#mustRunAfter.
    
    Please refer to https://docs.gradle.org/8.0.2/userguide/validation_problems.html#implicit_dependency for more details about this problem.
```
翻译一下，报错的意思就是**任务':app:compileOfficialDebugKotlin'使用任务':app:greendao'的输出，但没有声明显式或隐式依赖，并贴心的给出了几种解决办法和相关的gradle[链接](https://docs.gradle.org/8.0.2/userguide/validation_problems.html#implicit_dependency).**

修改一下build.gradle脚本，添加依赖关系，编译kotlin的任务依赖greendao任务，如下：
```groovy
tasks.whenTaskAdded { task ->
    if (task.name.matches("compile\w*Kotlin")) {
        task.dependsOn('greendao')
    }
}
```
然后再重新编译就可以编译通过✅了，最终的build.gradle脚本如下：

```groovy
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-android-extensions'
    id 'kotlin-kapt'
    id 'org.greenrobot.greendao'
}

greendao {
    schemaVersion 19
    daoPackage 'xxx'
    targetGenDir 'src/main/java'
}

//添加依赖关系
tasks.whenTaskAdded { task ->
    if (task.name.matches("compile\w*Kotlin")) {
        task.dependsOn('greendao')
    }
}

dependencies {
    implementation 'org.greenrobot:greendao:3.3.0'
}

```

# 参考资源
- [https://github.com/greenrobot/greenDAO](https://github.com/greenrobot/greenDAO)

- [# The project encountered errors after updating Gradle Version 7.6.1 to Gradle Version 8.0+](https://github.com/greenrobot/greenDAO/issues/1110)

- [https://docs.gradle.org/8.0.2/userguide/validation_problems.html#implicit_dependency](https://docs.gradle.org/8.0.2/userguide/validation_problems.html#implicit_dependency)


