### side + (header + main)

基于vue2 + ElementUI

完整代码

~~~vue
<template>
  <div>
    <el-container style="height: 100vh;">
        
        <el-scrollbar wrap-style="overflow-x:hidden;"><!--滚动条-->
        <!-- width="200px" 固定-->
        <!-- :width="sideWidth + 'px'"绑定变量 -->
        <!-- box-shadow: 2px 0 6px rgb(0 21 41 / 35%);:侧边栏阴影效果 -->
        <el-aside :width="sideWidth + 'px'" style="box-shadow: 2px 0 6px rgb(0 21 41 / 35%);">
        
        <!-- active-text-color="#ffd04b":导航栏点击高亮 -->
        <!-- overflow-x: hidden;: 解决导航栏左侧溢出导致参差不齐 -->
        <!-- background-color="rgb(48,65,86)":侧边栏颜色 -->
        <!-- :collapse-transition="false":关闭侧边栏自带的动画 -->
        <!-- :collapse="isCollapse":折叠属性 -->
        <!-- 属性要加在el-menu才有效例如overflow-y: hidden; 加在el-aside标签处不会生效 
		而加载el-menu则有效
		-->
       <!-- 即说el-aside只是一个边框如box-shadow: 2px 0 6px rgb(0 21 41 / 35%);加了这个有阴影效果 -->
        <el-menu 
        :default-openeds="['1', '3']"
        style="min-height: 100vh; overflow-x: hidden;overflow-y: hidden;"
        background-color="rgb(48,65,86)"
        text-color="#fff"
        active-text-color="#ffd04b"
        :collapse-transition="false"
        :collapse="isCollapse"
        >
        <div style="height: 60px; line-height: 60px;text-align: center;">
            <img src="../../assets/logo.png" alt="" style="width: 20px; position: relative;top: 5px; margin-right: 3px;">
            <b style="color: white;" v-show="!isCollapse">后台管理系统</b>
        </div>
        <el-submenu index="1">
            <template slot="title">
                <i class="el-icon-message"></i>
                <span slot="title">导航一</span>
            </template>
            <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
            <el-menu-item index="1-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="1-4">
            <template slot="title">选项4</template>
            <el-menu-item index="1-4-1">选项4-1</el-menu-item>
            </el-submenu>
        </el-submenu>
        <el-submenu index="2">
            <template slot="title">
                <i class="el-icon-menu"></i>
                <span slot="title">导航二</span>
            </template>
            <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="2-1">选项1</el-menu-item>
            <el-menu-item index="2-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
            <el-menu-item index="2-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="2-4">
            <template slot="title">选项4</template>
            <el-menu-item index="2-4-1">选项4-1</el-menu-item>
            </el-submenu>
        </el-submenu>
        <el-submenu index="3">
            <template slot="title">
                <i class="el-icon-setting"></i>
                <span slot="title">导航三</span>
            </template>
            <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="3-1">选项1</el-menu-item>
            <el-menu-item index="3-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
            <el-menu-item index="3-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="3-4">
            <template slot="title">选项4</template>
            <el-menu-item index="3-4-1">选项4-1</el-menu-item>
            </el-submenu>
        </el-submenu>
        </el-menu>
        
    </el-aside>
        </el-scrollbar>
    
    
    <el-container>
        <el-header style="font-size: 12px; border-bottom:1px solid #ccc;display: flex;">
            <div style="flex: 1; font-size: 18px;">
                <span :class="collapseBtnClass" style="cursor: pointer;" @click="collapse"></span>
            </div>
            <!-- cursor: pointer;:鼠标悬浮变小手 -->
        <el-dropdown style="width: 70px; cursor: pointer;">
            <span>王小虎</span>
            <i class="el-icon-arrow-down" style="margin-left: 5px"></i>
            <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>查看个人信息</el-dropdown-item>
            <el-dropdown-item>退出</el-dropdown-item>
            </el-dropdown-menu>
        </el-dropdown>
       
        </el-header>
        
        <el-scrollbar wrap-style="overflow-x:hidden;">
            <el-main style="padding-top: 10px ;scrollbar-width: thin;">
            <div class="button-collapse">
                <div style="margin: 10px 0;">
                <el-input style="width: 200px;" placeholder="请输入名称" suffix-icon="el-icon-search"></el-input>
                <el-button style="margin-left: 5px;" type="primary">搜索</el-button>
                </div>

                <div style="margin: 10px 0;">
                    <el-button type="primary" size="small">新增<i class="el-icon-circle-plus-outline"></i></el-button>
                    <el-button type="danger" size="small">批量删除<i class="el-icon-remove-outline"></i></el-button>
                    <el-button type="primary" size="small">导入<i class="el-icon-bottom"></i></el-button>
                    <el-button type="primary" size="small">导出<i class="el-icon-top"></i></el-button>
                </div>          
            </div>
            
            <div class="select-table">
                <el-table :data="tableData" border>
                    <el-table-column prop="date" label="日期" width="140">
                    </el-table-column>
                    <el-table-column prop="name" label="姓名" width="120">
                    </el-table-column>
                    <el-table-column prop="address" label="地址">
                    </el-table-column>
                    <el-table-column label="操作">
                        <template slot-scope="scope">
                            <el-button type="warning" @click="handleWaring(scope)" size="small">编辑<i class="el-icon-edit"></i></el-button>
                            <el-button type="danger" @click="handleDelete(scope)" size="small">删除<i class="el-icon-remove-outline"></i></el-button>
                        </template>
                    </el-table-column>
                </el-table>

                <div style="padding: 10px 0;">
                    <el-pagination
                    :page-sizes="[5, 10, 15, 20]"
                    :page-size="100"
                    layout="total, sizes, prev, pager, next, jumper"
                    :total="400">
                    </el-pagination>
                </div>
            </div>
        
        </el-main>
       </el-scrollbar>
        
    </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
    data() {
      const item = {
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      };
      return {
        tableData: Array(20).fill(item),
        isCollapse:false,
        sideWidth:200,
        collapseBtnClass:'el-icon-s-fold'
      }
    },
    methods:{
        collapse(){//点击收缩
            // alert("触发");
            this.isCollapse = !this.isCollapse;
            if(this.isCollapse){
                this.sideWidth = 64;
                this.collapseBtnClass = 'el-icon-s-unfold';
            }else{
                this.sideWidth = 200;
                this.collapseBtnClass = 'el-icon-s-fold';
            }
        }
    }
}
</script>

<style>
    .el-header {
        background-color: #B3C0D1;
        color: #333;
        line-height: 60px;
    }
    
    .el-aside {
        color: #333;
        /* background-color: #021936; */此处设置背景颜色不会生效
    }
    .button-collapse{//背景阴影
        width: 100%;
        background: #fff;
        border-radius: 6px;
        margin-top: 10px;
        padding-top: 2px;
        padding-bottom: 2px;
        box-shadow: 1px 1px 3px rgba(0, 0, 0, .2);
    }
    .select-table{//背景阴影
        width: 100%;
        background: #fff;
        border-radius: 6px;
        margin-top: 10px;
        /* padding-top: 5px; */
        padding-bottom: 13px;
        box-shadow: 1px 1px 3px rgba(0, 0, 0, .2);
    }
</style>
~~~

### 效果

![效果图](https://github.com/leyuan123/leyuan123.github.io/assets/126044735/2f4c9f47-f083-4dfd-8b9f-ce667f75c6c8)

### 解释

#### Template部分

- `<el-container style="height: 100vh;">`: 使用 Element UI 的容器组件，设置高度为全屏。 `100vh` 代表视口高度即占满全屏
- `<el-scrollbar wrap-style="overflow-x:hidden;">`: 使用滚动条组件并隐藏水平滚动条。
- `<el-aside :width="sideWidth + 'px'" style="box-shadow: 2px 0 6px rgb(0 21 41 / 35%);">`: 侧边栏组件，宽度绑定 `sideWidth` 变量，设置阴影效果。
- `<el-menu>`: 导航菜单组件，设置默认打开项、背景颜色、文字颜色、高亮颜色、折叠动画和折叠状态。
- `<el-submenu>`: 菜单子项组件，用于分组菜单项。
- `<el-header>`: 页头组件，包含收缩按钮和用户下拉菜单。
- `<el-scrollbar wrap-style="overflow-x:hidden;">`: 内容区滚动条，隐藏水平滚动条。
- `<el-main>`: 主内容区，包含搜索框、操作按钮和表格组件。
- `<el-table>`: 表格组件，展示数据。
- `<el-pagination>`: 分页组件，设置分页属性。

#### Script部分

- `data()`: 定义组件的初始数据。
  - `tableData`: 表格数据，包含日期、姓名和地址。
  - `isCollapse`: 控制侧边栏是否折叠。
  - `sideWidth`: 侧边栏宽度。
  - `collapseBtnClass`: 折叠按钮的类名。
  
- 
  `methods`: 定义组件的方法。

  - `collapse()`: 控制侧边栏的展开和折叠。

#### Style部分

- `.el-header`: 设置页头的样式，包括背景颜色、文字颜色和行高。
- `.el-aside`: 设置侧边栏的样式，注释掉背景颜色设置。
- `.button-collapse`: 设置操作按钮区的样式，包括宽度、背景色、边框半径、外边距、内边距和阴影。
- `.select-table`: 设置表格区的样式，包括宽度、背景色、边框半径、外边距、内边距和阴影。