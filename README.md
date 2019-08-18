### typetools
---
https://github.com/jhalterman/typetools

```java
interface Foo<T1, T2> {}
class Bar implements Foo<Integer, String> {}

Class<?>[] typeArgs = TypeResolver.resolveRawArguments(Foo.class, Bar.class);

assert typeArgs[0] == Integer.class;
assert typeArgs[1] == String.class;

Function<String> strToInt = s -> Integer.valueOf(s);
Class<?> typeArgs = TypeResolver.resolveRawArguments(Function.class, strToInt.getClass());

assert typeArgs[0] == String.class;
assert typeArgs[1] == Integer.class;


Comparator<String> comparator = String::compareToIgnoreCase;
Class<?> typeArg = TypeResolver.resolverRawArgument(Comparator.class, comparator.getClass());

assert typeArg == String.class;


interface Foo<T> {}
class Bar implements Foo<List<Integer>> {}

Type typeArgs = TypeResolver.reify(Foo.class, bar.class);

ParameterizedType paramType = (ParameterizedType) typeArgs;
Type[] actualTypeArgs = paramType.getActualTypeArgments();
ParameterizedType arg = (ParameterizedType)actualTypeArgs[0];










```

```
```

```
```


