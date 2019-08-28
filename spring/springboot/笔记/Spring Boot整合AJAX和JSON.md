提交方式为 POST 时，

​	JQuery Ajax 以 application/x-www-form-urlencoded 上传 JSON对象 ，

​			后端用 @RequestParam 或者Servlet 获取参数。

​	JQuery Ajax 以 application/json 上传 JSON字符串，

​			后端用 @RquestBody 获取参数。

后端用 @RequestParam 或者Servlet 获取参数。

JQuery Ajax 以 application/json 上传 JSON字符串，

后端用 @RquestBody 获取参数。

总结成表 

![img](https://img-blog.csdn.net/20180405152713112)


原文链接：https://blog.csdn.net/Edison_03/article/details/79826656





# 1.index

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.bootcss.com/jquery/2.1.1/jquery.min.js"></script>
    <script src="https://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
    <script src="js/index.js"></script>
    <title>Title</title>
</head>
<body>
<button id="btn" class="btn btn-success">an</button>
<div id="return">return</div>

</body>
</html>
```

# 2.javascript



```javascript
JQuery——AJAX（返回数据格式为application/x-www-form-urlencoded，将@RequestBody注解去掉）：
$(document).ready(function(){
  $("#btn").click(function(){
      $.post(
          "http://localhost:8080/area/1",
          '{"user":"py"}',//【注】json对象外要将上''
          function(data) {
              alert(data.name);
              $("#return").html(data.name)
          }
      );
  });
});

原生ajax（返回数据格式为application/json，将@RequestBody注解去掉）：
$(document).ready(function(){
    // 绑定点击事件
    $("#btn").click(function(){
        $.ajax({
            url:"http://localhost:8080/area/1",
            contentType:"application/json;charset=UTF-8",
            data:'{"id":"1","name":"py"}',//【注】json对象外要将上''
            dataType:"json",
            type:"post",
            success:function(data){
                $("#return").html(data.name)
            }
        });
    });
});
```


# 3.controller类

```java
@ResponseBody
@RequestMapping("/area/{id}")
@RequestWrapper
public Area login(@PathVariable("id") Integer id, @RequestBody String user){
    Area area=serchService.SerchGet(id);
    System.out.println(area);
    System.out.println(user);
    return area;
}
```

# 4 javebeanlei

```java
public class Ajax {
    private Integer id;
    private String name;
    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }



    @Override
    public String toString() {
        return "Ajax{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}

```



# 5.地址

http://localhost:8080/area/1

