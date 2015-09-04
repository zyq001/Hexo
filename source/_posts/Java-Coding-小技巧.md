title: Coding 小技巧  
date: 2015-07-04 23:31:49  
tags: [tips]  
categories: [tips]   
thumbnail: /images/Tipstb.jpg  
banner: /images/Tips.jpg  
---

1. 如何打印数组不用for--println without foreach  

就算debug用的再6，写代码中不可避免地要打印一些东西，高级语言横行的时代，Java数组打印居然还要自己foreach，不过还好各种容器类如List重写了toString函数，可以直接打印，那么问题就简单了，把数组转换成List。而且查阅源码，发现


- `Arrays.asList(T... a)`其实是new了一个ArrayList，而且直接把数组的指针赋值过去的，没有多余地进行ArrayCopy。不过既然是模板，那么基本类型的数组是没法用的，，  
- `Arrays.toString(各种类型包括Object[])`后来发现这个，这个重载了好多，不仅支持Object数组，还支持各种基本类型数组，那就直接拿来用吧！  
**总结:**  
如果是基本类型，如int[] arr,这样打：`System.out.println(Arrays.toString(arr));`   
如果是String[]或者其他Object[] arr,这样打：`System.out.println(Arrays.asList(arr));` 