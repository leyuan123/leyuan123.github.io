### 直接前端导出数据成Excel文件

#### 1.1安装`xlsx`库

首先安装`xlsx`库

```bash
npm install xlsx
```

#### 1.2在Vue组件中使用`xlsx`导出Excel

~~~vue
<template>
  <div>
    <el-button type="primary" @click="downloadData" style="margin-bottom: 10px">
      下载数据
    </el-button>
    <el-table :data="tableData" style="width: 100%">
      <el-table-column label="课题名称" width="180">
        <template slot-scope="scope">
          <i class="el-icon-time"></i>
          <span style="margin-left: 10px">{{ scope.row.TopicName }}</span>
        </template>
      </el-table-column>

      <el-table-column label="姓名" width="180">
        <template slot-scope="scope">
          <el-popover trigger="hover" placement="top">
            <p>学生姓名: {{ scope.row.name }}</p>
            <p>
              是否通过: {{
                scope.row.status == "0"
                  ? "未评分"
                  : scope.row.status == "1"
                  ? "通过"
                  : "未通过"
              }}
            </p>
            <div slot="reference" class="name-wrapper">
              <el-tag size="medium">{{ scope.row.name }}</el-tag>
            </div>
          </el-popover>
        </template>
      </el-table-column>

      <el-table-column label="评分">
        <template slot-scope="scope">
          <el-select v-model="scope.row.status" placeholder="请选择">
            <el-option label="未评分" value="0"></el-option>
            <el-option label="通过" value="1"></el-option>
            <el-option label="未通过" value="2"></el-option>
          </el-select>
        </template>
      </el-table-column>

      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)">提交</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import * as XLSX from "xlsx";

export default {
  data() {
    return {
      tableData: [
        // 示例数据
        {
          TopicName: "课题1",
          name: "学生1",
          status: "0",
        },
        {
          TopicName: "课题2",
          name: "学生2",
          status: "1",
        },
      ],
    };
  },
  methods: {
    handleEdit(index, row) {
      console.log("提交:", row);
      // 处理提交逻辑，例如调用API更新数据
    },
    downloadData() {
      const data = this.tableData.map(row => ({
        "课题名称": row.TopicName,
        "姓名": row.name,
        "状态": row.status == "0" ? "未评分" : row.status == "1" ? "通过" : "未通过"
      }));

      const worksheet = XLSX.utils.json_to_sheet(data);
      const workbook = XLSX.utils.book_new();
      XLSX.utils.book_append_sheet(workbook, worksheet, "Sheet1");

      XLSX.writeFile(workbook, "tableData.xlsx");
    },
  },
};
</script>

<style scoped>
/* 添加你的样式 */
</style>

~~~

- 解释

**1.安装 `xlsx` 库**：使用 `npm install xlsx` 安装 `xlsx` 库。

**2.引入 `xlsx` 库**：在 `script` 部分引入 `xlsx`。

**3.下载数据方法 `downloadData`**：

- 将 `tableData` 映射为需要导出的格式。
- 使用 `XLSX.utils.json_to_sheet` 方法将数据转换为 Excel 工作表。
- 创建一个新的工作簿 `XLSX.utils.book_new()`。
- 将工作表添加到工作簿中 `XLSX.utils.book_append_sheet`。
- 使用 `XLSX.writeFile` 方法将工作簿保存为 `tableData.xlsx` 文件。

**4.详细解释downloadData**

~~~javascript
downloadData() {
      const data = this.tableData.map(row => ({
        "课题名称": row.TopicName,
        "姓名": row.name,
        "状态": row.status == "0" ? "未评分" : row.status == "1" ? "通过" : "未通过"
      }));

      const worksheet = XLSX.utils.json_to_sheet(data);
      const workbook = XLSX.utils.book_new();
      XLSX.utils.book_append_sheet(workbook, worksheet, "Sheet1");

      XLSX.writeFile(workbook, "tableData.xlsx");
    },
  },
~~~

- 数据替换

~~~JavaScript
downloadData() {
  const data = this.tableData.map(row => ({
    "课题名称": row.TopicName,
    "姓名": row.name,
    "状态": row.status == "0" ? "未评分" : row.status == "1" ? "通过" : "未通过"
  }));

~~~

1.使用 `map` 方法遍历 `tableData` 数组，将每一行数据映射为一个新对象。

2.这个新对象的键为 `"课题名称"`, `"姓名"` 和 `"状态"`，值分别对应 `row.TopicName`, `row.name` 和 `row.status`。

3.`row.status` 的值通过三元运算符进行转换：如果 `status` 为 `"0"` 则显示 `"未评分"`，如果 `status` 为 `"1"` 则显示 `"通过"`，否则显示 `"未通过"`。

- 转换为工作表

~~~JavaScript
  const worksheet = XLSX.utils.json_to_sheet(data);
~~~

1.使用 `XLSX.utils.json_to_sheet(data)` 方法将刚才生成的 `data` 数组转换为一个 Excel 工作表。

2.`json_to_sheet` 方法会将 JavaScript 对象数组转换为一个可用于 Excel 的工作表对象。

- 创建工作薄

~~~javascript
  const workbook = XLSX.utils.book_new();
~~~

1.使用 `XLSX.utils.book_new()` 方法创建一个新的工作簿对象。

2.工作簿是 Excel 文件的基本结构，可以包含多个工作表。

- 添加工作表到工作薄

~~~javascript
  XLSX.utils.book_append_sheet(workbook, worksheet, "Sheet1");
~~~

1.使用 `XLSX.utils.book_append_sheet(workbook, worksheet, "Sheet1")` 方法将前面创建的工作表 `worksheet` 添加到工作簿 `workbook` 中。

2.`Sheet1` 是这个工作表的名字，你可以根据需要进行更改。

- 写入并保存文件

~~~javascript
  XLSX.writeFile(workbook, "tableData.xlsx");
}
~~~

1.使用 `XLSX.writeFile(workbook, "tableData.xlsx")` 方法将工作簿保存为一个 Excel 文件。

2.`"tableData.xlsx"` 是保存的文件名，可以根据需要进行更改。

3.这个方法会触发浏览器下载动作，将文件下载到用户的电脑中。

#### 总结

该方法的整个流程如下：

1. 将 `tableData` 转换为符合需求的对象数组。
2. 使用 `xlsx` 库将对象数组转换为 Excel 工作表。
3. 创建一个新的工作簿。
4. 将工作表添加到工作簿中。
5. 将工作簿保存为 Excel 文件，并触发浏览器下载。

