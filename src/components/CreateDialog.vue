<template>
    <div>
        <!-- 新增对话框 -->
        <el-dialog title="新增数据" :visible.sync="dialogVisible" width="30%" :before-close="handleClose">
            <!-- 这里放置新增数据的表单等内容 -->
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="编号">
                    <el-input v-model="form.No" type="number" :controls="false"></el-input>
                </el-form-item>
                <el-form-item label="姓名" type="text">
                    <el-input v-model="form.name"></el-input>
                </el-form-item>
                <el-form-item label="性别">
                    <el-select v-model="form.sex">
                        <el-option value=""></el-option>
                        <el-option value="女">女</el-option>
                        <el-option value="男">男</el-option>
                    </el-select>
                </el-form-item>
                <el-form-item label="部门">
                    <el-input v-model="form.department" type=""text></el-input>
                </el-form-item>
                <el-form-item label="出生日期">
                    <el-date-picker v-model="form.birthday" type="date" placeholder="选择日期">
                    </el-date-picker>
                </el-form-item>
                <el-form-item label="工资">
                    <el-input v-model="form.salary" type="number" :controls="false"></el-input>
                </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button @click="cancel">取 消</el-button>
                <el-button type="primary" @click="submitForm">确 定</el-button>
            </span>
        </el-dialog>
    </div>
</template>

<script>

export default {
    name: "CreateDialog",
    data() {
        return {
            dialogVisible: false,
            form: {
                No: "",
                name: "",
                sex: "",
                salary: "",
                department: "",
                birthday: new Date()
            }
        };
    },
    methods: {
        handleClose(done) {
            if (!this.formHasErrors) {
                this.dialogVisible = false;
            }
        },
        cancel:function(){
            this.dialogVisible = false;
            this.form.No = "";
            this.form.name = "";
            this.form.sex = "";
            this.form.salary = "";
            this.form.department = "";
            this.birthday = new Date();
        },
        submitForm() {
            this.dialogVisible = false;
            this.form.birthday = this.form.birthday.toLocaleDateString();
            this.$emit("create",this.form);
            this.cancel();
        },
    }
};
</script>