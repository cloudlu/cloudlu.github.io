##Hibernate Batch Insert/Update
https://vladmihalcea.com/2015/03/18/how-to-batch-insert-and-update-statements-with-hibernate/

##What does Batch Insert/Update means for SQL
http://stackoverflow.com/questions/1006969/why-are-batch-inserts-updates-faster-how-do-batch-updates-work

##Hibernate Avoid OOM with Spring Data
int size = 1000;
List<List<T>> subs = Lists.partition(orignalList, size);
for (List<T> sub : subs) {
    repo.save(sub);
}

##Hibernate Fetch Size
findByKeyIn(List<String> key);
hibernate.jdbc.fetch_size 1000

##Hibernate cache seq or use application generated ID
Cache Seq with default 50 make application 10 times faster when insert 8k objects in batch
Use UUID as ID can be faster compare to cache sequence.
