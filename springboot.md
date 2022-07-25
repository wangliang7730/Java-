# springboot

[toc]

### 基本注解

POST /url 创建  
DELETE /url/xxx 删除 
PUT /url/xxx 更新
GET /url/xxx 查看

##### @Configuration

告诉springboot这是一个配置类

##### @Bean

给容器中添加组件，方法名为组件id，返回类型就是组件类型，返回值就是容器示例

@Controller

@Autowired

##### @component

web开发，提供3个@Component注解衍生注解（功能一样）取代
@Repository(“名称”)：dao层
@Service(“名称”)：service层
@Controller(“名称”)：web层

@Autowired：自动根据类型注入
@Qualifier(“名称”):指定自动注入的id名称

@Resource(“名称”)
@ PostConstruct 自定义初始化
@ PreDestroy 自定义销毁

@ResponseBody的作用其实是将java对象转为json格式的数据。

@PathVariable 映射 URL 绑定的占位符

@Repository接口的一个实现类交给spring管理

@PathVariable（路径变量）、@RequestHeader（获取请求头）、@ModelAttribute、@RequestParam（获取请求参数）、@MatrixVariable（矩阵变量）、@CookieValue（获取cookie值）、@RequestBody（获取请求体）



![image-20220703072609792](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703072609792.png)

![image-20220703084325596](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703084325596.png)

![image-20220703084458752](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703084458752.png)

![image-20220703090434250](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703090434250.png)







![image-20220703093203774](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703093203774.png)



![image-20220703142321139](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703142321139.png)



![image-20220703150639798](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703150639798.png)

![image-20220703150742973](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703150742973.png)

![image-20220703150836068](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703150836068.png)

**请求转发是request的方法，重定向是response的方法**



![image-20220703151704744](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703151704744.png)

导包

![image-20220703152534012](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703152534012.png)

![image-20220703153624106](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703153624106.png)

![image-20220703153638749](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703153638749.png)

![image-20220703154528453](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703154528453.png)

![image-20220703154702800](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703154702800.png)

![image-20220703160218971](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703160218971.png)

![image-20220703160430552](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703160430552.png)

![image-20220703162327934](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703162327934.png)

![image-20220703162434987](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703162434987.png)

<img src="C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703162910019.png" alt="image-20220703162910019" style="zoom:67%;" />



![image-20220703162953192](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703162953192.png)

![image-20220703173509628](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703173509628.png)



![image-20220703173920382](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703173920382.png)

![image-20220703174447057](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703174447057.png)

![image-20220703175246718](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703175246718.png)

![image-20220703175511259](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703175511259.png)

![image-20220703181340803](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703181340803.png)

![image-20220703182118024](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703182118024.png)

![image-20220703182713342](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703182713342.png)

![image-20220703183200270](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220703183200270.png)

![image-20220704072636102](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220704072636102.png)

![image-20220704073120733](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220704073120733.png)

![image-20220704073425505](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220704073425505.png)

![image-20220704073442584](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220704073442584.png)

![image-20220704073458788](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220704073458788.png)

![image-20220704073525576](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220704073525576.png)

![image-20220704080103304](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220704080103304.png)

![image-20220704081015603](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220704081015603.png)









### 小技巧

##### lombok

简化javabean开发

##### dev-tools

热更新





