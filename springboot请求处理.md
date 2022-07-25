# spring boot请求处理

[toc]



## 获取处理函数

mappedHandler = this.getHandler(processedRequest);

- 初始化RequestMappingHandlerMapping
- 初始化RequestMappingHandlerAdapter

## 参数返回值处理

- 获取HandlerMethod，组装HandlerExecutionChain对象
- 获取HandlerAdapter
- 使用HandlerAdapter执行HandlerMethod

## 整体流程

遍历所有的HandlerMapping对象，找到匹配当前请求对应的HandlerMethod
将HandlerMethod包装成HandlerExecutionChain对象
根据HandlerMethod找到HandlerAdapter
HandlerAdapter执行HandlerMethod
