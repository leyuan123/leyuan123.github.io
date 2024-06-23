### 接收 JSON 数据到对象

> 你可以将请求体中的 JSON 数据直接映射到一个 Java 对象

- 前端代码

~~~ javascript
axios.post("https://yapi.pro/mock/356423/student/p1", {
    id: '2002',
    name: 'John Doe',
    age: 20,
    gender: 'Male',
    result: 'A'
}).then((result) => {
    alter("success");
}).catch((error) => {
    alter.("error");
});
~~~

- 后端controller代码

~~~java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/student")
public class StudentController {

    @Autowired
    private StudentService studentService;

    @PostMapping("/p1")
    public Result getStudent(@RequestBody Student request) {
        
        return Result.success();
    }
}

~~~

### 使用 `@RequestParam` 接收 URL 参数

> **如果数据是通过 URL 参数传递的**，你可以使用 `@RequestParam` 注解

- 前端代码

~~~javascript
axios.get("https://yapi.pro/mock/356423/student/p1", {
    params: {
        id: '2002'
    }
}).then((result) => {
    alter("success");
}).catch((error) => {
    alter.("error");
});
~~~

- 后端controller代码

~~~java
@RestController
@RequestMapping("/student")
public class StudentController {

    @Autowired
    private StudentService studentService;

    @GetMapping("/p1")
    public Reuslt getStudent(@RequestParam String id) {
        
        return Reuslt.success();
    }
}
~~~

###  使用 `@PathVariable` 接收路径变量

> **如果数据是通过 URL 路径传递的**，你可以使用 `@PathVariable` 注解

- 前端代码

~~~javascript
axios.get(`https://yapi.pro/mock/356423/student/p1/2002`).then((result) => {
    alter("success");
}).catch((error) => {
    alter("error");
});
~~~

- 后端controller代码

~~~java
@RestController
@RequestMapping("/student")
public class StudentController {

    @Autowired
    private StudentService studentService;

    @GetMapping("/p1/{id}")
    public Reuslt getStudent(@PathVariable String id) {
        
        return Reuslt.success();
    }
}
~~~

### 使用 `@ModelAttribute` 接收表单数据

> **如果数据是通过表单提交的**，你可以使用 `@ModelAttribute` 注解

- 前端代码

~~~javascript
const formData = new FormData();
formData.append('id', '2002');
formData.append('name', 'John Doe');
formData.append('age', 20);
formData.append('gender', 'Male');
formData.append('result', 'A');

axios.post("https://yapi.pro/mock/356423/student/p1", formData).then((result) => {
    alter("success");
}).catch((error) => {
    alter("error");
});
~~~

- 后端controller代码

~~~java
@RestController
@RequestMapping("/student")
public class StudentController {

    @Autowired
    private StudentService studentService;

    @PostMapping("/p1")
    public Reuslt getStudent(@ModelAttribute Student request) {
        
        return Reuslt.success();
    }
}
~~~

### get

如果你要发送一个带有路径参数的 `GET` 请求来根据 `id` 查询特定资源，可以直接将 `id` 作为路径的一部分，并使用 `axios.get` 发送请求。这里是一个示例，展示如何发送这样的请求：

#### 示例代码

假设你的 API 的 URL 是 `https://example.com/api/users/{id}`，你需要查询用户 ID 为 `123` 的信息。

```
const userId = 123;
const apiUrl = `https://example.com/api/users/${userId}`;

axios.get(apiUrl)
    .then(response => {
        console.log('Response:', response.data);
    })
    .catch(error => {
        console.error('Error:', error);
    });
```

#### 解析

1. URL：

   ```
   https://example.com/api/users/123
   ```

   - 这里 `123` 是路径参数，表示用户的 ID。

2. **没有配置对象**：只发送基础的 `GET` 请求。

#### 示例总结

- **路径参数**：`userId` 被包含在 URL 中，用于指定资源路径。

如果你还需要添加查询参数或其他配置，可以使用 `axios.get` 的第二个参数配置对象。例如，假设你还想添加一个查询参数 `status` 和一个请求头 `Authorization`：

```
const userId = 123;
const apiUrl = `https://example.com/api/users/${userId}`;

axios.get(apiUrl, {
    params: {
        status: 'active'
    },
    headers: {
        'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
    },
    timeout: 5000  // 可选，设置请求超时时间为5秒
})
    .then(response => {
        console.log('Response:', response.data);
    })
    .catch(error => {
        console.error('Error:', error);
    });
```

#### 解析

1. **URL**：`https://example.com/api/users/123`

   - 这里 `123` 是路径参数，表示用户的 ID。

2. **配置对象**：

   ```
   {
       params: {
           status: 'active'  // 查询参数，将附加到 URL 上，最终的 URL 为 https://example.com/api/users/123?status=active
       },
       headers: {
           'Authorization': 'Bearer YOUR_ACCESS_TOKEN'  // 请求头，通常用于身份验证
       },
       timeout: 5000  // 请求超时时间，单位为毫秒（5秒）
   }
   ```

#### 示例总结

- **路径参数**：`userId` 被包含在 URL 中，用于指定资源路径。
- **查询参数** (`params`)：`status=active` 被附加到 URL 上。
- **请求头** (`headers`)：添加了 `Authorization` 头。
- **请求超时时间** (`timeout`)：设置为 5000 毫秒（即 5 秒）。

这段代码会发送一个 `GET` 请求到 `https://example.com/api/users/123?status=active`，并在请求头中包含授权令牌。如果请求成功，响应数据会在控制台输出；如果发生错误，错误信息会在控制台输出。

### get和put请求的区别

~~~text
在 PUT 请求中，通常有一个请求体 data，并且可以通过 params 对象传递 URL 参数。与 GET 请求不同，PUT 请求的第二个参数是请求体，第三个参数是配置对象。
即第三个参数相当于get的第二个参数
~~~

#### 示例

- get

~~~javascript
axios.get('https://example.com/api/resource', {
  params: {
    id: 123
  }
}).then(response => {
  console.log(response.data);
}).catch(error => {
  console.error('There was an error!', error);
});

~~~

- put

~~~javascript
axios.put('https://example.com/api/resource', {
  // request body data
  name: 'New Name'
}, {
  params: {
    id: 123
  }
}).then(response => {
  console.log(response.data);
}).catch(error => {
  console.error('There was an error!', error);
});
//
axios.put("https://yapi.pro/mock/356423/teacher/p2", null, {
  params: {
    TopicName: this.TopicName
  }
}).then((result) => {
  alert(result.data.data);
  row.topicName = result.data.data.topicName;
  row.difficulty = result.data.data.difficulty;
  row.topicInfo = result.data.data.topicInfo;
}).catch((error) => {
  console.error("There was an error!", error);
});

~~~

#### 示例解释

1. **URL**：`https://yapi.pro/mock/356423/teacher/p2`。

2. **请求体**：由于没有请求体数据，传递 `null`。

   - 这是发送到服务器的实际数据。在 `PUT` 请求中，这通常是你想要更新的资源的新数据。你可以在这里传递一个 JavaScript 对象，`axios` 会自动将其转换为 JSON 格式发送。

3. 配置对象
   - `params` 对象中的参数 `TopicName` 会被添加到 URL 的查询字符串中。

   - 这个参数是一个配置对象，允许你配置请求的各种选项，例如 URL 参数（query parameters）、请求头（headers）、超时（timeout）等。

   - 下面是一个使用 `axios` 发送 `PUT` 请求的例子，其中包括了配置对象，配置了各种选项，例如 URL 参数（query parameters）、请求头（headers）、和超时（timeout）。

     ```
     axios.put("https://example.com/api/resource", {
         // 请求主体数据
         name: "New Name",
         description: "Updated Description"
     }, {
         // 配置对象
         params: {
             id: 123  // URL 查询参数
         },
         headers: {
             'Authorization': 'Bearer YOUR_ACCESS_TOKEN',  // 请求头
             'Content-Type': 'application/json'
         },
         timeout: 5000  // 请求超时时间，单位为毫秒
     })
     .then(response => {
         console.log('Response:', response.data);
     })
     .catch(error => {
         console.error('Error:', error);
     });
     ```

     ### 解析

     1. **URL**：`https://example.com/api/resource`

     2. 请求主体数据：

        ```
        {
            name: "New Name",
            description: "Updated Description"
        }
        ```

     3. 配置对象：

        ```
        {
            params: {
                id: 123  // 将附加到 URL 上，最终的 URL 为 https://example.com/api/resource?id=123
            },
            headers: {
                'Authorization': 'Bearer YOUR_ACCESS_TOKEN',  // 请求头，通常用于身份验证
                'Content-Type': 'application/json'  // 请求的内容类型，默认为 JSON
            },
            timeout: 5000  // 请求超时时间，单位为毫秒（5秒）
        }
        ```

     ### 示例总结

     - **URL 查询参数** (`params`): `id=123` 将被附加到 URL 上。
     - **请求头** (`headers`): 添加了 `Authorization` 和 `Content-Type` 头。
     - **请求超时时间** (`timeout`): 设置为 5000 毫秒（即 5 秒）。

     这个例子展示了如何使用 `axios` 的配置对象来配置 `PUT` 请求的各种选项，包括 URL 查询参数、请求头和超时设置。如果服务器返回响应，则会在控制台输出响应数据；如果发生错误，则会在控制台输出错误信息。

### delete请求

使用 Axios 发送 DELETE 请求的方法与发送其他类型的请求类似，但需要注意 DELETE 请求通常不会发送请求体（body），而是通过 URL 参数传递信息。下面是一个基本的示例：

```
axios.delete('https://api.example.com/resource', {
  params: {
    id: '12345'
  }
}).then((response) => {
  console.log('Deleted successfully');
}).catch((error) => {
  console.error('Error deleting:', error);
});
```

#### 解释代码：

1. **`axios.delete` 方法**：用于发送 DELETE 请求。
2. **URL**：指定要删除的资源的 URL。例如，`'https://api.example.com/resource'` 是一个示例 URL。
3. **配置对象**：
   - **`params`**：指定 URL 查询参数。在 DELETE 请求中，通常会把需要删除的资源的标识（如 ID）通过 URL 参数传递给服务器。
4. **`.then` 和 `.catch`**：处理异步操作的成功和失败情况。

在上面的示例中，`params` 对象中的 `id: '12345'` 将作为 URL 的查询参数，添加到 DELETE 请求中。服务器端可以根据这些参数来识别和删除相应的资源。

#### 注意事项：

在 `axios` 中，`axios.delete` 方法的第二个参数是配置对象，不是请求体。这与 `axios.post` 和 `axios.put` 不同，后者的第二个参数是请求体数据，第三个参数是配置对象。

具体来说，当你在 `axios.delete` 方法中传递第二个参数时，它是配置对象，包含 URL 查询参数、请求头等。

#### 例子

假设你要发送一个带有查询参数的 `DELETE` 请求，并且配置对象包含 `params`，则代码如下：

```
axios.delete('https://api.example.com/resource', {
  params: {
    id: '12345'
  }
})
.then(response => {
  console.log('Response:', response.data);
})
.catch(error => {
  console.error('Error:', error);
});
```

#### 解析

- **URL**：`https://api.example.com/resource`

- 配置对象：

  ```
  {
    params: {
      id: '12345'  // 查询参数，将附加到 URL 上，最终的 URL 为 https://api.example.com/resource?id=12345
    }
  }
  ```

这个代码发送一个 `DELETE` 请求到 `https://api.example.com/resource?id=12345`，没有请求体。

#### 确认省略的是配置参数

在 `axios.delete` 请求中，没有专门用于请求体的参数。第二个参数总是配置对象。这意味着当你传递一个对象作为第二个参数时，`axios` 将其视为配置对象，包含查询参数、请求头等。

#### 扩展：带有请求头的 DELETE 请求

如果你想要在 `DELETE` 请求中添加请求头，可以在配置对象中添加 `headers`：

```
axios.delete('https://api.example.com/resource', {
  params: {
    id: '12345'
  },
  headers: {
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
  }
})
.then(response => {
  console.log('Response:', response.data);
})
.catch(error => {
  console.error('Error:', error);
});
```

#### 例子总结

- **配置对象**：用于设置查询参数（`params`）、请求头（`headers`）等。
- **没有请求体**：`axios.delete` 不支持直接传递请求体数据，所有配置都是通过第二个参数的配置对象完成的。

这样可以明确地看出，在 `axios.delete` 请求中，第二个参数始终是配置对象，不是请求体。

### 注意返回数据的利用

~~~json
{
  code: 0,
  msg: 'success',
  data: [
    {
      topicName: '计算机',
      difficulty: 'easy',
      topicInfo: 'hello'
    }
  ]
}

~~~

错误访问data

~~~JavaScript
axios.put("https://yapi.pro/mock/356423/teacher/p2",{
    TopicName: row.TopicName
}).then((result) => {
    console.log(result.data.data[0].topicName); // 访问数组第一个元素的 topicName 属性
    // 如果需要赋值给 row 对象
    row.topicName = result.data.data.topicName;
    row.difficulty = result.data.data.difficulty;
    row.topicInfo = result.data.data.topicInfo;
}).catch((error) => {
    console.error("There was an error!", error);
});

~~~

正确访问data

根据这个结构，`result.data.data` 是一个数组，其中包含一个对象，对象的属性包括 `topicName`、`difficulty` 和 `topicInfo`。因此，要访问 `topicName`，需要通过数组索引访问

~~~JavaScript
axios.put("https://yapi.pro/mock/356423/teacher/p2",{
    TopicName: row.TopicName
}).then((result) => {
    console.log(result.data.data[0].topicName); // 访问数组第一个元素的 topicName 属性
    // 如果需要赋值给 row 对象
    row.topicName = result.data.data[0].topicName;
    row.difficulty = result.data.data[0].difficulty;
    row.topicInfo = result.data.data[0].topicInfo;
}).catch((error) => {
    console.error("There was an error!", error);
});

~~~



### 示例

> vue2 代码

- 配置端口转发(vue.config.js)

~~~js
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:8080', // 你的后端服务器地址
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
}

~~~

>**`target`**：指定代理的目标地址，即你的后端服务器地址和端口。
>
>**`changeOrigin`**：如果需要，可以设置为 `true` 以更改请求头中的 `Host` 字段，使其与目标服务器匹配。
>
>**`pathRewrite`**：用于重写请求路径。上面的例子中，`'^/api'` 被替换为空字符串，因此 `/api/employees` 将被代理到 `http://localhost:8080/employees`。

- 注意

~~~text
在 vue.config.js 中配置代理时，'^/api' 中的 ^ 符号是一个正则表达式的语法，表示匹配路径的开始。因此，'^/api' 表示只匹配以 /api 开头的路径。如果去掉 ^ 符号，路径中只要包含 /api 就会被匹配。

是否需要 ^ 符号取决于你的需求。如果你想严格匹配以 /api 开头的路径，那么 ^ 是必要的。如果你希望匹配路径中包含 /api 的任何部分，那么可以去掉 ^ 符号。
~~~



~~~vue
<template>
  <div>
    <h1>员工分页查询</h1>
    <form @submit.prevent="fetchData">
      <label for="name">姓名:</label>
      <input type="text" v-model="name" id="name" />

      <label for="gender">性别:</label>
      <select v-model="gender" id="gender">
        <option value="">请选择</option>
        <option value="1">男</option>
        <option value="2">女</option>
      </select>

      <label for="begin">开始日期:</label>
      <input type="date" v-model="begin" id="begin" />

      <label for="end">结束日期:</label>
      <input type="date" v-model="end" id="end" />

      <button type="submit">查询</button>
    </form>

    <div v-if="pageBean">
      <h2>查询结果</h2>
      <p>总记录数: {{ pageBean.total }}</p>
      <ul>
        <li v-for="emp in pageBean.data" :key="emp.id">{{ emp.name }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      page: 1,
      pageSize: 10,
      name: '',
      gender: '',
      begin: '',
      end: '',
      pageBean: null
    };
  },
  methods: {
    fetchData() {
      axios.get('/api/employees', {
        params: {
          page: this.page,
          pageSize: this.pageSize,
          name: this.name,
          gender: this.gender,
          begin: this.begin,
          end: this.end
        }
      })
      .then(response => {
        this.pageBean = response.data;
      })
      .catch(error => {
        console.error("There was an error!", error);
      });
    }
  }
};
</script>

<style scoped>
/* 样式可以根据需要进行调整 */
form {
  margin-bottom: 20px;
}

label {
  display: block;
  margin: 5px 0;
}

input, select {
  display: block;
  margin-bottom: 10px;
}
</style>

~~~

- 关于'/api/employees'

~~~text
在 Vue.js 或 JavaScript 中，URL 字符串通常使用单引号 ' 或双引号 "，两者是等价的，具体选择取决于个人或团队的编码风格和习惯。所以你可以将 '/api/employees' 改为 "/api/employees"，效果是一样的。
~~~

> java代码

~~~java
@Slf4j
@RequestMapping("/emps")
@RestController
public class EmpController {
    @Autowired
    private EmpService empService;

    @GetMapping
    public Result page(@RequestParam(defaultValue = "1") Integer page,
                       @RequestParam(defaultValue = "10") Integer pageSize, String name, Short gender,
                       @DateTimeFormat(pattern = "yyyy-MM-dd") LocalDate begin,
                       @DateTimeFormat(pattern = "yyyy-MM-dd") LocalDate end){

        log.info("分页查询,参数:{},{},{},{},{},{}",page,pageSize,name,gender,begin,end);
        //调用service分页查询
        PageBean pageBean = empService.page(page,pageSize,name,gender,begin,end);
        return Result.success(pageBean);
    }
}
~~~

