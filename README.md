## 介绍

该项目演示了一个在循环依赖下导致maven传递依赖失效（或者说用错scope）的问题

## 特别注意

1. 由于整个dependency-problem项目的modules(dependency3和dependency4)存在循环依赖，所以直接对dependency-problem编译会报错
2. 由于dependency3和dependency4存在循环依赖，所以需要先把循环依赖移除，成功install到本地，然后再加上，这样才能保证2个包都可以install成功
3. 全过程建议使用maven的offline模式

## 验证
1. 可以通过在dependency-root下执行`mvn dependency:tree -o | grep json-path`来验证。当json-path的scope为test时，验证传递依赖是否失效
2. 也可以通过运行dependency-root项目下的Main.java里的main方法，来验证传递依赖是否失效。不过可能会因为循环依赖报错报错，需要关闭annotation processing

```
❯ mvn dependency:tree -o | grep json-path
[INFO]    +- com.jayway.jsonpath:json-path:jar:2.4.0:test
```