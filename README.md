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

assert paramType.getRawType() == Foo.class;
assert arg1.getRawType() == List.class;
assert arg1.getActualTypeArguments()[0] == Integer.class;


class Entity<ID extends Serializable> {
  ID id;
  void setId(ID id) {}
}
class SomeEntity extends Entity<Long> {}
Type fieldType = Entity.class.getDeclaredField("id").getGenericType();
Type mutatorType = Entity.class.getDeclaredMethod("setId", Serializable.class).getGenericParameterTypes()[0];

assert TypeResolver.resolveRawClass(fieldType, SomeEntity.class) == Long.class;
assert TypeResolver.resolveRawClass(mutatorType, SomeEntity.class) == Long.class;


class Device {}
class Router extends Device {}

class GenericDAO<T, ID extends Serializable> {
  protected Class<T> persistentClass;
  protected Class<ID> idClass;
  
  private GenericDAO() {
    class<?> typeArguments = TypeResolver.resolveRawArguments(GenericDAO.class, getClass());
    this.persistentClass = (Class<T>) typeArguments[0];
    this.idClass = (Class<ID>) typeArguments[1];
  }
}

class DeviceDAO<T extends Device> extends GenericDAO<T, Long> {}
class RouterDAO extends DeviceDAO<Router> {}


RouterDAO routerDAO = new RouterDAO();
assert routerDAO.persistentClass == Router.class;
assert routerDAO.idClass == Long.class;

TypeResolver.enableCache();
TypeResolver.disableCache();

interface ExtraFunction<T, R, Z> extends Function<T, R>{}
ExtraFunction<String, Integer, Long> strToInt = s -> Integer.value(s);
Class<?>[] typeArgs = TypeResolver.resolveRawArguments(Function.class, strToInt.getClass());

assert typeArgs[0] == String.class;
assert typeArgs[1] == Integer.class;
assert typeArgs[2] == Unknown.class;

org.osgi.framework.system.packages.extra=sun.reflect
```

```
```

```
```


