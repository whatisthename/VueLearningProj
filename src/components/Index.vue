<template>
    <el-container style="height: 100vh">
      <el-header>
        <el-form :inline="true" :model="filterInfo">
          <el-form-item label="姓名">
            <el-input v-model="filterInfo.name"></el-input>
          </el-form-item>
          <el-form-item label="性别">
            <el-select v-model="filterInfo.sex">
              <el-option value=""></el-option>
              <el-option value="女">女</el-option>
              <el-option value="男">男</el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="所属部门">
            <el-input v-model="filterInfo.department"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button @click="onFilter">查询</el-button>
            <el-button @click="onReset">重置</el-button>
          </el-form-item>
          <el-form-item>
            <!-- 触发对话框的按钮 -->
            <el-button type="primary" @click="onCreateClick">新增</el-button>
          </el-form-item>

        </el-form>

      </el-header>
      <el-container>
        <el-aside width="200px">
          <el-menu default-active="2">
            <el-menu-item index="2">
              <i class="el-icon-menu"></i>
              <span slot="title">导航二</span>
            </el-menu-item>
            <el-menu-item index="3" disabled>
              <i class="el-icon-document"></i>
              <span slot="title">导航三</span>
            </el-menu-item>
            <el-menu-item index="4">
              <i class="el-icon-setting"></i>
              <span slot="title">导航四</span>
            </el-menu-item>
          </el-menu>
        </el-aside>
        <el-main class="container">
          <el-table :data="resultTableData" >
            <el-table-column fixed prop="No" label="No" width="150">
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column prop="sex" label="性别" width="50">
            </el-table-column>
            <!-- <el-table-column prop="city" label="市区" width="120">
          </el-table-column> -->
            <el-table-column prop="department" label="部门" width="300">
            </el-table-column>
            <el-table-column prop="birthday" label="出生年月" width="300">
            </el-table-column>
            <el-table-column prop="salary" label="工资" width="100">
            </el-table-column>
            <el-table-column label="操作" width="300">
              <template #default="scope">
                <el-button type="text" @click="onDeleteClick(scope.row)">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-main>
      </el-container>
      <CreateDialog ref="dialog" @create="onCreate"></CreateDialog>
    </el-container>
</template>

<script>
import CreateDialog from "./CreateDialog.vue";
export default {
  name: 'Index',
  components: {
    "CreateDialog": CreateDialog
  },
  data() {
    return {
      originData: [
        {
          No: "1",
          name: "ZRR",
          sex: "女",
          salary: "10000",
          department: "开发",
          birthday: new Date("2024/05/18").toLocaleDateString()
        },
        {
          No: "2",
          name: "qwe",
          sex: "女",
          salary: "123432",
          department: "开发",
          birthday: new Date("2024/05/18").toLocaleDateString()
        },
        {
          No: "3",
          name: "abc",
          sex: "女",
          salary: "7879879",
          department: "销售",
          birthday: new Date("2024/05/18").toLocaleDateString()
        },
        {
          No: "4",
          name: "jkl",
          sex: "男",
          salary: "6687",
          department: "销售",
          birthday: new Date("2024/05/18").toLocaleDateString()
        },
      ],
      resultTableData: [],
      filterInfo: {
        name: "",
        sex: "",
        department: ""
      }
    }
  },
  methods: {
    onFilter: function () {
      this.resultTableData = this.originData.filter((item) => {
        if (this.filterInfo.name != "" && item.name.search(this.filterInfo.name) >= 0) {
          console.log("filter name:" + this.filterInfo.name);
          return true;
        }
        if (this.filterInfo.sex == "" || item.sex == this.filterInfo.sex) {
          return true;
        }
        if (this.filterInfo.department != "" && item.department.search(this.filterInfo.department) > 0) {
          return true;
        }
      });
    },
    onReset: function () {
      this.filterInfo.name = "";
      this.filterInfo.sex = "";
      this.filterInfo.department = "";
      // reset table data
      this.resultTableData = [];
    },
    onCreateClick: function () {
      // this.dialogVisible = true;
      // console.log(this);
      // console.log(CreateDialog.data());
      this.$refs.dialog.dialogVisible = true;
      // console.log();
    },
    onCreate: function (newItem) {
      var copyNewItem = Object.assign({}, newItem);
      this.originData.push(copyNewItem);

    },
    onDeleteClick: function (deleteItem) {
      var originIndex = this.originData.indexOf(deleteItem);
      var resultIndex = this.resultTableData.indexOf(deleteItem);
      this.originData.splice(originIndex, 1);
      this.resultTableData.splice(resultIndex, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  /* display: flex; */
  justify-content: center; 
  align-items: center; 
  height: 100vh;
}
 
.control {
  display: inline-block;
}
</style>
