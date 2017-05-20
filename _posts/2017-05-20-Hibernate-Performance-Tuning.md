---
layout: post
title:  "Hibernate性能相关配置"
date:   2017-05-20 22:14:00
categories: Java
tags: Hibernate Performance
---

* content
{:toc}
JPA简化了Java程序员的开发，不过想用好它却是非常的不容易，这里总结一下我用Hibernate的一些心得。

## Hibernate Batch Insert/Update
主要配置：
```Java
properties.put("hibernate.order_inserts", "true");
properties.put("hibernate.order_updates", "true");
properties.put("hibernate.jdbc.batch_size", 30); //10-50
properties.put("hibernate.jdbc.batch_versioned_data", "true");
```
具体参考:https://vladmihalcea.com/2015/03/18/how-to-batch-insert-and-update-statements-with-hibernate/
Batch底层的具体实现可以参考：http://stackoverflow.com/questions/1006969/why-are-batch-inserts-updates-faster-how-do-batch-updates-work

## Hibernate Avoid OOM with Spring Data
在save之前先手动分割列表，可以直接使用save方法而不用flush
```Java
int size = 1000;
List<List<T>> subs = Lists.partition(orignalList, size);
for (List<T> sub : subs) {
    repo.save(sub);
}
```
## Hibernate Fetch Size
当一次性获取较多对象时，最好设置fetch size
```Java
findByKeyIn(List<String> key);
properties.put("hibernate.jdbc.fetch_size", 1000); 
```
## Hibernate cache Sequence or use application generated ID
Cache Seq with default 50 make application 10 times faster when insert 8k objects in batch
Use UUID as ID can be faster compare to cache sequence.

## Hibernate使用Cache
参考：https://dzone.com/articles/all-about-hibernate-second

## Avoid N+1 Selection
使用Fetch Join来避免集合属性的N次读取问题
