---
title: 关于Android中的转场动画
date: 2017-04-28
tags: android
---

转场动画即在Activity之间切换时执行的动画，是为了提高用户体验的整体美感

<!-- more -->

### 简单转场动画

启动Activity的方法

	Intent intent = new Intent(context, LoginActivity.class);
    context.startActivity(intent, ActivityOptions.makeSceneTransitionAnimation((Activity) context).toBundle());

这里就改变了一个地方，之前startActivity方法是只需要专递intent就可以，现在就是在startActivity方法增加了一个参数，使用转场动画启动下一个Activity。

在onCreate方法中添加下面两句话，第一句是设置启动时动画运行的时间，第二句是退出时动画运行的时间，单位都是毫秒，我们的应用一般都会有个BaseActivity，可以将这两句话加在BaseActivity中，可以避免在每个Activity中添加。

	@Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        getWindow().setEnterTransition(new Explode().setDuration(500));
        getWindow().setExitTransition(new Explode().setDuration(500));
        super.onCreate(savedInstanceState);
    }

最后还需要修改主题样式，在对应Activity使用的主题上设置下面属性

	<item name="android:windowContentTransitions">true</item>


这样最简单的转场动画就实现了

### 炫酷转场动画

要想实现更加炫酷的转场动画就需要在启动下一个Activity之前做更多的准备了

makeSceneTransitionAnimation方法其实还可以传递参数，不信你安装Ctrl进去看看，后面传递的是一个可变长参数（暂且把它理解成数组），这个参数就是来设置Activity跳转之间的共享元素的，具体方法为

首先需要在xml中给共享的View都设置相同的标识

	android:transitionName="btn_logo_register"

然后修改Activity启动

	Intent intent = new Intent(context, LoginActivity.class);
    context.startActivity(intent, 
		ActivityOptions.makeSceneTransitionAnimation((Activity) context, 
		Pair.create(((View)mLoginBtn), "btn_logo_register")).toBundle());

然后你会发现设置了相同transitionName属性的两个View在Activity之间跳转是有了那么一缕联系

更多炫酷的动画就是要巧妙的设计共享元素这个参数了

### 我遇到的坑

&emsp;&emsp;在使用了转场动画去启动下一个Activity后，执行finish()方法关闭Activity回退时，发现Activity是退回来了，但是屏幕始终都无法点击（当时我还以为我手机坏了呢），手机上的实体键和虚拟键都还能用。后来我又发现使用手机上的虚拟键回退Activity时，屏幕是能点击，然后我就研究了下onBackPressed()这个方法，因为点击手机上的虚拟键时是调用这个方法结束Activity的，在onBackPressed()方法里执行了finishAfterTransition()这样一个方法，我看到这个方法的名字就明白了，大概就是说在执行完转场后finish嘛，所以在使用转场动画的方启动Activity时手动结束Activity要使用finishAfterTransition()。

尽管finishAfterTransition()最后还是调用了finish()方法。毕竟在执行之前做了判断啊