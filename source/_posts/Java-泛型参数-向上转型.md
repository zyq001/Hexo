title: Java 泛型参数 向上转型  
date: 2014-06-03 09:54:27  
tags: [Java]  
categories: [算法]   
---
根据现在的了解，java泛型默认是不支持向上转型的，但是可以通过**泛型参数**实现**向上转型**

`List<List<Integer>> re = new ArrayList<ArrayList<Integer>>(); `//这样编译通过 类型不匹配，无法转型

`List<? extends List<Integer>> re = new ArrayList<ArrayList<Integer>>();`//但是这样就可以，因为添加了泛型参数，任何继承List的类都没有问题