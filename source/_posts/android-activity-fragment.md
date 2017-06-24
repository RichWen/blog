---
title: android中Activity重建后Fragment重复创建
date: 2017-04-27
tags: android
---

今天写项目遇到一个问题，就是一个Activity里面有多个Fragment需要管理，当屏幕旋转时多个Fragment会出现重叠的现象，原因是因为旋转屏幕时Activity会重建，造成Fragment多次创建产生重叠。

<!-- more -->
其实这个问题一句话也是可以解决的，就是在Android项目的配置文件中给相应的Activity加上   

    android:configChanges="orientation|screenSize|keyboardHidden"

这句话的意思就是让Activity不要重建，屏幕旋转的问题解决，但是···

但是如果就这样的解决问题，那我今天就将它不会记录下来了，因为Activity重建不只是在屏幕发生旋转时才会有的，其他情况也是有可能的，比如：**应用退到后台了**、**突然来了个电话**（也是退到后台了），像这样的情况我不知道上面那句话行不行，但是就是因为这个才引发我的思考，还能不能有其他的方法呢。

在Activity发生重建之前，保存当前的数据，在Activity再次创建时恢复

1.首先是保存Activity销毁之前的数据

	@Override  
	protected void onSaveInstanceState(Bundle outState) {  
	    outState.putInt("current",currentFragment);  
	    super.onSaveInstanceState(outState);  
	} 

2.重写onSaveInstanceState方法，将当先显示的是第几个Fragment用outState保存起来。
然后在onCreate方法里做还原操作

	@Override
    protected void onCreate(Bundle savedInstanceState) {
    	super.onCreate(savedInstanceState);
    	setContentView(R.layout.activity_main);
    	fragmentManager = getFragmentManager();
       	// 从savedInstanceState中恢复数据, 如果没有数据需要恢复savedInstanceState为null
       	if (savedInstanceState != null) {
        //当Activity发生重建时还原Fragment
        mMyLifeFragment = (MyLifeFragment) fragmentManager.findFragmentByTag("MyLifeFragment");
        mFindFragment = (FindFragment) fragmentManager.findFragmentByTag("FindFragment");
        mMessageFragment = (MessageFragment) fragmentManager.findFragmentByTag("MessageFragment");
        if(mMessageFragment!=null){
            fragmentManager.beginTransaction().hide(mMessageFragment).commit();
        }
        if (mFindFragment!=null){
            fragmentManager.beginTransaction().hide(mFindFragment).commit();
        }
        if(mMyLifeFragment!=null){
            //说明Activity发生了重建，设置之前保存的currentFragment
            fragmentManager.beginTransaction().hide(mMyLifeFragment).commit();
            addOrShowFragment(savedInstanceState.getInt("current"));
        }
       }else{
           //没有数据可以还原，初始化主显示界面
           addOrShowFragment(SHOW_LIFE);
       }
   	}


&emsp;&emsp;上面的mMyLifeFragment、mFindfragment、mMessageFragment这三个Fragment是我要在Activity中显示的，addOrShowFragment方法就是用来向FragmentManager添加Fragment或显示FragmentManager里面的Fragment，里面传递的参数就是要显示的是第一个Fragment。

这样实现了即使Activity重建也不会影响显示了。

该项目开源在github上 [imemory](https://github.com/ZhanghangNice/imemory)