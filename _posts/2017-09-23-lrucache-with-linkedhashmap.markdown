---
layout: post
Title: "LinkedHashMap을 이용한 LRUCache의 구현"
Author: bosco lyu
Date:   September 27, 2017  
Meta: "IT"
---

<img src="/images/fulls/03.jpg" class="fit image">

## LRUCache algorithms
LRUCache는 (Least-Recently-Used Cache)의 약자이다. 최근에 가장 적게 사용된 item을 Cache에서 제거하는 알고리즘이다.
참조 문서 : http://en.wikipedia.org/wiki/Cache_algorithms

## LinkedHashMap VS HashMap

* HashMap
    * 내부의 Entry 구현을 보면 collision(충돌)이 발생했을 경우에만 Entry의 next 변수를 이용해서 linked list를 이용하도록 구현했다.

* HashMap에 item을 넣는 put 메소드

```java
public V put(K key, V value) {
    if (key == null)
        return putForNullKey(value);
    int hash = hash(key.hashCode());
    int i = indexFor(hash, table.length);
    for (Entry e = table[i]; e != null; e = e.next) {
        Object k;
        if (e.hash == hash && ((k = e.key) == key || key.equals(k))) {
            V oldValue = e.value;
            e.value = value;
            e.recordAccess(this);
            return oldValue;
        }
    }

    modCount++;
    addEntry(hash, key, value, i);
    return null;
}
```
  
```java
    void addEntry(int hash, K key, V value, int bucketIndex) {
        Entry e = table[bucketIndex];
        table[bucketIndex] = new Entry(hash, key, value, e);
        if (size++ >= threshold)
            resize(2 * table.length);
    }
```

* LinkedHashMap
    * HashMap을 상속받아서 구현한 클래스이다. 내부의 Entry 구현을 보면 기본적으로 Entry에서 before, after 변수를 가지고 있어서 Entry를 linked list 구조로 별도 연결을 하고 있다.


```java
    void addEntry(int hash, K key, V value, int bucketIndex) {
        createEntry(hash, key, value, bucketIndex);

        // Remove eldest entry if instructed, 
        // else grow capacity if appropriate
        Entry eldest = header.after;
        if (removeEldestEntry(eldest)) {
            removeEntryForKey(eldest.key);
        } else {
            if (size >= threshold)
                resize(2 * table.length);
        }
    }

    void createEntry(int hash, K key, V value, int bucketIndex) {
        HashMap.Entry old = table[bucketIndex];
        Entry e = new Entry(hash, key, value, old);
        table[bucketIndex] = e;
        e.addBefore(header);
        size++;
    }

```

LinkedHashMap을 생성하는 시점에 accessOrder값을 true로 설정해주어야 한다.
true로 설정하면 access할 때마 linkedlist의 맨 앞으로 이동시키는 로직이 동작하고, false로 설정하거나 설정하지 않으면 삽입 순서대로 linked list가 생성되므로 LRU 알고리즘으로 동작하지 않는다. 


   
```java
    public V get(Object key) {
        Entry e = (Entry)getEntry(key);
        if (e == null)
            return null;
        e.recordAccess(this);
        return e.value;
    }
```

```java
        private void remove() {
            before.after = after;
            after.before = before;
        }

        private void addBefore(Entry existingEntry) {
            after  = existingEntry;
            before = existingEntry.before;
            before.after = this;
            after.before = this;
        }

        void recordAccess(HashMap m) {
            LinkedHashMap lm = (LinkedHashMap)m;
            if (lm.accessOrder) {
                lm.modCount++;
                remove();
                addBefore(lm.header);
            }
        }
```

LinkedHashMap 클래스는 removeEldestEntry 메소드를 가지고 있어서 가장 오래된 Entry를 삭제할 수 있는 기능이 있다. 하지만 소스를 보면 메소드 안에서 실제 Entry를 삭제하는 코드는 없는 것을 발견할 수 있다.
무조건 false 를 반환하도록 되어 있다.

 해당 메소드를 overriding해서 삭제 여부를 boolean 값으로 반환할 뿐임

```java
    protected boolean removeEldestEntry(Map.Entry eldest) {
        return false;
    }
```

* LinkedHashMap을 이용한 LRUCache의 구현
    * LinkedHashMap의 removeEldestEntry의 메소드 안에는 실제 Entry를 삭제하는 코드가 없으므로 해당 메소드를 overriding해야 한다. 메소드 안에서 Map의 크기가 cache의 사이즈보다 커지면 삭제하라는 true값을 반환하도록 구현하면 LinkedHashMap에서 알아서 가장 오래된 Entry값을 삭제한다.
