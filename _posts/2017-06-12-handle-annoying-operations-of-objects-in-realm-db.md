---
layout: post
title: Handle annoying operations of objects in Realm DB
date: 2017-06-12
category: iOS & watchOS
tags: 
summary: Update objects in Realm is annoying. Could we operate objects in Realm without being aware of the existence of Realm?
published: true
---

# Problem

Update value of object in Realm DB is annoying because the task should be within a writing transition. 

# Solution

Extend the Realm's Object class to provide convient methods to do these things:

- `update`: to set/update properties' values. 
- `remove`: to remove object from Realm

```swift
// RealmHelper.swift
import RealmSwift

extension Object {
    // Update property value in Realm
    func update(_ property: String, value: Any?) {
        let realm = try! Realm()
        try! realm.write {
            self.setValue(value, forKey: property)
        }
    }
    
    // Remove object from Realm
    func remove() {
        let realm = try! Realm()
        try! realm.write {
            realm.delete(self)
        }
    }
}
```

<!--<script src="https://gist.github.com/herrkaefer/6e3ac0e561daaac8f3887166fee2bf11.js"></script>
-->