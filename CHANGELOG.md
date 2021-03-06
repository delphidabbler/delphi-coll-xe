# Change Log

All notable changes to this project will be documented in this file. As of the first alpha release of v2.0 this project adheres to [Semantic Versioning](http://semver.org/).

## Unreleased

### Changes before project fork

There following is a guesstimate of the changes made to the project from v1.2 until the the project was forked. This list is not guaranteed to be complete or totally accurate!

* Various renamings:
    * `TEnexAssociativeCollection<TKey,TValue>` as `TAssociation<TKey,TValue>`;
    * `IEnexAssociativeCollection<TKey,TValue>` as `IAssociation<TKey,TValue>`;
    * `TEnexCollection<T>` as `TSequence<T>`;
    * `IEnexCollection<T>` as `ISequence<T>`;
    * `TCollection<T>` as `TContainer<T>`;
    * `ICollection<T>` as  `IContainer<T>`; 
    * `TAbstractCollection` as `TAbstractContainer`;
    * `TAbstractCollection<T>` as  `TAbstractContainer<T>`; 
    * `TOperableCollection<T>` as `TCollection<T>`;
    * `IOperableCollection<T>` as `ICollection<T>`;
    * `[NonSerializable]` attribute as `[NonSerialized]`.
* Removed `GroupedBy<T>()` extended operation added in v1.1.

### Changes since project fork

* Fixed unit tests to enable compilation and to prevent test running from crashing when running some tests. Many of the changes were required because of the interface and class name changes noted above. **Note:** No attempt was made to make any failed tests pass or to complete missing tests -- the changes were simple to get the test runner compiled and running.
* Documentation changes:
    * Added documentation recovered from former project wiki on *GoogleCode*.
    * Rewrote read-me.
    * Added credits file listing contributors.
    * Revised license information in light of project fork.
    * Formatted change log in markdown.
    * Removed outdated help file and its source documents.
* Fixed problem with project options that was causing AV fault in Delphi XE IDE. 
* Removed modeling files.
* Fixed *Samples* project to work around an apparent Delphi XE compiler bug.
* New batch file to delete temporary files from source tree.
* Build number in library version information no longer auto-increments on each build.

--------

**Below are the releases made on the original *pavkam/delphi-coll* project. These releases are undated did not follow the Semantic Versioning model.**

--------

##  Major Release: 1.2

* New unit `Collections.Serialization`. Includes:
    1. `TSerializer` - a semi-abstract class that implementes generic serialization.
    2. `TDeserializer` - a semi-abstract class that implements generic deserialization.
    3. `ISerializable` - an interface can be implemented by classes that need to override the default serialization.
    4. `TInputContext`/`TOutputContext` - two facade objects that only expose a few operations to classes through `ISerializable`.
    5. `[NonSerializable]` - the attribute to marks field that should not be serialized.
    6. Two concrete implementations for serialization in implementation section!
* Some documentation fixes all over the place.
* Removed the `ICollectionMap<TKey, TValue>` interface. It made no sense in the hierarchy. Its methods were split between the two interfaces that inherited it.
* Added a new interface `ILinkedList<T>` currently implemented by `TLinkedList<T>` and `TSortedLinkedList<T>`.
* Removed `Copy` methods from `TList<T>`.
* Removed sorting, reversing and copy methods from `TLinkedList<T>`. That was a mistake anyway.
* Added `TAbstractSet<T>` from which all sets derive.
* Added `TAbstractStack<T>` from which all stacks derive.
* Added `TAbstractQueue<T>` from which all queues derive.
* Added `TAbstractDictionary<T>` from which all dictionaries derive. This allowed us to remove a lot of duplicated code.
* Added `TAbstractList<T>` from which `TList<T>` derives.
* Added `TAbstractLinkedList<T>` derived from `TAbstractList<T>` from which `TLinkedList<T>` derives.
* `TSortedList<T>` extends `TList<T>` now while `TSortedLinkedList<T>` extends `TLinkedList<T>`. Removed a lot of duplicated code.
* Removed `ISortedList<T>`. There's nothing I can put in there to make it useful.
* `TLinkedList<T>` and `TSortedLinkedList<T>` implement `IQueue<T>` and `IStack<T>`. A linked list can be used as both these collections transparently.
* `TCollection<T>` base class supports versioning out of the box.
* `TEnumerator<T>` base class was renamed to `TAbstractEnumerator<T>` and completely revamped. It is now much more simple to extend and also provides version checking out of the box.
* `TForwardingEnumerator<T>` is a special class that uses another enumerator as base.
* Renamed `IEnexGroupingCollection<TKey, T>` as `IGrouping<TKey, T>`.
* Rewrote all enumerators in the package to use the new interface.
* Introduced a new non-generic `TAbstractCollection`. `TAbstractCollection<T>` derives from it.
* Added `IOperableCollection<T>` that exposes `Add`, `AddAll`, `Remove`, `RemoveAll`, `Contains`, `ContainsAll` and `Clear` methods.
* Added `TOperableCollection<T>` with default implementation of `IOperableCollection<T>`. All simple types adjusted accordingly.
* `IList<T>.Insert(Collection)` renamed to `InsertAll`. `Add(Collection)` renamed to `AddAll`.
* `ILinkedList<T>.AddLast(Collection)` renamed to `AddAllLast`. `AddFirst` renamed to `AddAllFirst`;
* New `TAbstractMap<TKey, TValue>` collection which is a base class for all associative maps.
* All collections now have only 3 constructors:
    1. The default parameterless one.
    2. The one that accepts the rule set (or sets for associative).
    3. The one that accepts the rule set(s) and additional information that can be:
        1. Sorting of elements/keys.
        2. Sorting of keys and sorting of values.
        3. Initial capacity.
        4. Initial capacity and sorting of elements/keys.
* Reworked the interface of `IBag<T>` to accommodate the new changes.
    
## Minor Release: v1.1.1
                                                                                             
* All lists and dictionaries now posses a `ExtractAt` or `Extract` or `ExtractKey`, `ExtractValue` methods. These function exactly as remove but do not trigger cleanup for objects.
* Fix: `TObjectMultiMap` required a class for it's value type parameter.
* Fix: `RemoveKey`/`RemoveValue` for `Bidi` dictionaries were not calling the cleaning handler.

## Major Release: v1.1

* Started a new project: `Samples`. A few samples have been added for your delight.
* Implemented `T(Object)LinkedDictionary<TKey, TValue>` that used a hash/linked list approach. Guarantees insert order preservation of elements.
* Implemented `T(Object)LinkedSet<T>` that used a hash/linked list approach. Guarantees insert order preservation of elements.
* `TBitSet`, a new Word-only type that uses an internal array of bits.
* New unit `Collection.BidiDictionaries` contains a number of dictionary types that enforce both key to value and value to key rules.
    * `TBidiDictionary<TKey, TValue>`
    * `TSortedBidiDictionary<TKey, TValue>`
    * `TDoubleSortedDictionary<TKey, TValue>`
* Added a new unit: `Collections.Dynamic`. This unit exposes a simple Member record that allows generating selectors for class/record members.
* `TView` is a small type that can hold a number of fields/properties from a object or record. Look at it as anonymous classes in C#. It's not that pretty but it does the job in some cases.
* Implement `T(Object)SortedLinkedList<T>`. This class uses a linked list to store its elements. It also implements `IList` interface and provides access to the index based functions (slow).      
* Added `ISortedSet<T>` interface now implemented by `TSortedSet<T>`.
* Added three new overloads to `Op.Select` (one with preset output type, one for `TValue` output and one for `TView` output).
* New `GroupedBy<T>()` extended operation and `IEnexGroupingCollection<TKey, T>`.
* Removed `IUnorderedList<T>`. All lists implement `IList<T>` now (that includes `Insert`!).
* `IList<T>` now includes `Insert()`.
* Renamed `IOrderedList<T>` into `ISortedList<T>`.
* `TLinkedStack<T>` now uses an internal linked list and not the much "loved" `TLinkedList` class. This should bring quite some speed improvements into the game.
* `TLinkedQueue<T>` now uses an internal linked list and not the much "loved" `TLinkedList` class. This should bring quite some speed improvements into the game.
* `TLinkedList<T>` was completely rewritten. It's no longer .NET-like, it looks just like a simple `TList<T>` but stores its elements in a linked list. A lot of indexing methods are supported but are dead slow!
* `TArraySet<T>` is not a sorted set. It's been optimized.
* `TSortedList<T>`'s methods have been optimized to use binary search.
* Optimized `TList<T>.Add(collection)` a lot. Should be a big boost to all dependent functions.
* Updated multiple tests. Added missing test cases for `TArraySet<T>`.
* Fixed a few bugs related to `IndexOf` in empty collections. Regression tests added.
* Fixed an error in `TDictionary<TKey, TValue>` and `THashSet<T>` where initial capacity size was set to zero.
* Fixed `TSortedList.Copy` to also copy the ascending/descending flag from the original list.
* Fixed some documentation (removed "cleaning" references).
* Fixed a bug in all dictionary implementations related to the way values were replaced. Memory leaks would appear. Regression tests added.
* Fixed a bug in all list implementations related to the way values were replaced. Memory leaks would appear. Regression tests added.

## Minor Release: v1.0.1

* Do not expose `AreEqual`, `Compare` and `GetHashCode` in `TRules<T>`.
* Add protected methods `ElementsAreEqual`, `CompareElements`, `GetElementHashCode` to `TEnexCollection<T>`.
* Add protected methods `KeysAreEqual`, `CompareKeys`, `GetKeyHashCode` to `TEnexAssociativeCollection<TKey, TValue>`.
* Add protected methods `ValuesAreEqual`, `CompareValues`, `GetValueHashCode` to `TEnexAssociativeCollection<TKey, TValue>`.
* Do not use `ElementRules`, `KeyRules` and `ValueRules` in code directly.
* Define `EArgumentNilException` if RTL version is less than 22 (2010).
* Fixed grammar and spelling errors (by Denisa Ilascu).
 
## Major Release: v1.0

* First public version!
* The following units are provided
    * `Collections.Base`
    * `Collections.Lists`
    * `Collections.Queues`
    * `Collections.Stacks`
    * `Collections.Sets`
    * `Collections.Dictionaries`
    * `Collections.Bags`
    * `Collections.MultiMaps`
    * `Collections.BidiMaps`
* Documentation is up.
* Everything is tested.
