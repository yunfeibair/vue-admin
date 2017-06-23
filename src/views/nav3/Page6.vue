<template>
	<section>
		<!--工具条-->
		<el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
			<el-form :inline="true" :model="filters">
				<el-form-item>
					<el-input v-model="filters.name" placeholder="姓名"></el-input>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" v-on:click="getUsers">查询</el-button>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" @click="handleAdd">新增</el-button>
				</el-form-item>
			</el-form>
		</el-col>

		<!--列表-->
		<el-table :data="users" highlight-current-row v-loading="listLoading" @selection-change="selsChange" style="width: 100%;">
			<el-table-column type="selection" width="55">
			</el-table-column>
			<el-table-column type="index" width="60">
			</el-table-column>
			<el-table-column prop="name" label="姓名" width="120" sortable>
			</el-table-column>
			<el-table-column prop="sex" label="性别" width="100" :formatter="formatSex" sortable>
			</el-table-column>
			<el-table-column prop="age" label="年龄" width="100" sortable>
			</el-table-column>
			<el-table-column prop="birth" label="生日" width="120" sortable>
			</el-table-column>
			<el-table-column prop="addr" label="地址" min-width="180" sortable>
			</el-table-column>
			<el-table-column label="操作" width="150">
				<template scope="scope">
					<el-button size="small" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
					<el-button type="danger" size="small" @click="handleDel(scope.$index, scope.row)">删除</el-button>
				</template>
			</el-table-column>
		</el-table>

		<!--工具条-->
		<el-col :span="24" class="toolbar">
			<el-button type="danger" @click="batchRemove" :disabled="this.sels.length===0">批量删除</el-button>
			<el-pagination layout="prev, pager, next" @current-change="handleCurrentChange" :page-size="20" :total="total" style="float:right;">
			</el-pagination>
		</el-col>

		<!--编辑界面-->
		<el-dialog title="编辑" v-model="editFormVisible" :close-on-click-modal="false">
			<el-form :model="editForm" label-width="80px" :rules="editFormRules" ref="editForm">
				<el-form-item label="姓名" prop="name">
					<el-input v-model="editForm.name" auto-complete="off"></el-input>
				</el-form-item>
				<el-form-item label="性别">
					<el-radio-group v-model="editForm.sex">
						<el-radio class="radio" :label="1">男</el-radio>
						<el-radio class="radio" :label="0">女</el-radio>
					</el-radio-group>
				</el-form-item>
				<el-form-item label="年龄">
					<el-input-number v-model="editForm.age" :min="0" :max="200"></el-input-number>
				</el-form-item>
				<el-form-item label="生日">
					<el-date-picker type="date" placeholder="选择日期" v-model="editForm.birth"></el-date-picker>
				</el-form-item>
				<el-form-item label="地址">
					<el-input type="textarea" v-model="editForm.addr"></el-input>
				</el-form-item>
			</el-form>
			<div slot="footer" class="dialog-footer">
				<el-button @click.native="editFormVisible = false">取消</el-button>
				<el-button type="primary" @click.native="editSubmit" :loading="editLoading">提交</el-button>
			</div>
		</el-dialog>

		<!--新增界面-->
		<el-dialog title="案件录入" v-model="addFormVisible" size="large" :close-on-click-modal="false">
			<el-form  ref="form" :model="form" label-width="80px" @submit.prevent="onSubmit" style="margin:20px auto 0;width:60%;">
				<el-form-item label="姓名">
					<el-input v-model="form.name"></el-input>
				</el-form-item>
				<el-form-item style="display: inline-block" label="性别">
					<el-col :span="24">
						<el-select v-model="form.region" placeholder="请选择性别">
							<el-option label="男" value="shanghai"></el-option>
							<el-option label="女" value="beijing"></el-option>
						</el-select>
					</el-col>
				</el-form-item>
				<el-form-item style="display: inline-block;margin-left: 104px" label="案件类型">
					<el-col :span="24">
						<el-select v-model="form.type" placeholder="请选择案件类型">
							<el-option label="刑侦类" value="shanghai"></el-option>
							<el-option label="治安类" value="beijing"></el-option>
							<el-option label="救助类" value="1"></el-option>
							<el-option label="纠纷类" value="2"></el-option>
							<el-option label="突发类" value="3"></el-option>
						</el-select>
					</el-col>
				</el-form-item>
				<el-form-item style="display: inline-block" label="报警时间">
					<el-col :span="24">
						<el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
					</el-col>
				</el-form-item>
				<el-form-item style="display: inline-block;margin-left: 104px" label="接警人">
					<el-col :span="24">
						<el-select v-model="form.types" placeholder="请选择接警人">
							<el-option label="王小虎" value="shanghai"></el-option>
							<el-option label="王大虎" value="beijing"></el-option>
							<el-option label="李明" value="1"></el-option>
							<el-option label="姚大帅哥" value="2"></el-option>
							<el-option label="赵五" value="3"></el-option>
						</el-select>
					</el-col>
				</el-form-item>
				<el-form-item label="报警方式">
					<el-input v-model="form.way"></el-input>
				</el-form-item>
				<el-form-item label="现住址">
					<el-input v-model="form.pepole"></el-input>
				</el-form-item>
				<el-form-item label="简要案情">
					<el-input type="textarea" v-model="form.desc"></el-input>
				</el-form-item>
				<el-form-item label="处理结果">
					<el-input type="textarea" v-model="form.desc1"></el-input>
				</el-form-item>
			</el-form>

			<div slot="footer" style="text-align: center" class="dialog-footer">
				<el-button @click.native="addFormVisible = false">取消</el-button>
				<el-button type="primary" @click.native="addSubmit" :loading="addLoading">立即录入</el-button>
			</div>
		</el-dialog>
	</section>
</template>

<script>
    import util from '../../common/js/util'
    import NProgress from 'nprogress'
    import { getUserListPage, removeUser, batchRemoveUser, editUser, addUser } from '../../api/api';

    export default {
        data() {
            return {
                filters: {
                    name: ''
                },
                users: [],
                total: 0,
                page: 1,
                listLoading: false,
                sels: [],//列表选中列

                editFormVisible: false,//编辑界面是否显示
                editLoading: false,
                editFormRules: {
                    name: [
                        { required: true, message: '请输入姓名', trigger: 'blur' }
                    ]
                },
                //编辑界面数据
                editForm: {
                    id: 0,
                    name: '',
                    sex: -1,
                    age: 0,
                    birth: '',
                    addr: ''
                },

                addFormVisible: false,//新增界面是否显示
                addLoading: false,
                addFormRules: {
                    name: [
                        { required: true, message: '请输入姓名', trigger: 'blur' }
                    ]
                },
                //新增界面数据
                form: {
                    name: '',
                    region: '',
                    date1: '',
                    way:'',
                    type:[],
                    date2: '',
                    pepole: '',
                    type: [],
                    resource: '',
                    desc: '',
                    desc1:''
                }

            }
        },
        methods: {
            //性别显示转换
            formatSex: function (row, column) {
                return row.sex == 1 ? '男' : row.sex == 0 ? '女' : '未知';
            },
            handleCurrentChange(val) {
                this.page = val;
                this.getUsers();
            },
            //获取用户列表
            getUsers() {
                let para = {
                    page: this.page,
                    name: this.filters.name
                };
                this.listLoading = true;
                NProgress.start();
                getUserListPage(para).then((res) => {
                    this.total = res.data.total;
                    this.users = res.data.users;
                    this.listLoading = false;
                    NProgress.done();
                });
            },
            //删除
            handleDel: function (index, row) {
                this.$confirm('确认删除该记录吗?', '提示', {
                    type: 'warning'
                }).then(() => {
                    this.listLoading = true;
                    NProgress.start();
                    let para = { id: row.id };
                    removeUser(para).then((res) => {
                        this.listLoading = false;
                        NProgress.done();
                        this.$notify({
                            title: '成功',
                            message: '删除成功',
                            type: 'success'
                        });
                        this.getUsers();
                    });
                }).catch(() => {

                });
            },
            //显示编辑界面
            handleEdit: function (index, row) {
                this.editFormVisible = true;
                this.editForm = Object.assign({}, row);
            },
            //显示新增界面
            handleAdd: function () {
                this.addFormVisible = true;
                this.addForm = {
                    name: '',
                    sex: -1,
                    age: 0,
                    birth: '',
                    addr: ''
                };
            },
            //编辑
            editSubmit: function () {
                this.$refs.editForm.validate((valid) => {
                    if (valid) {
                        this.$confirm('确认提交吗？', '提示', {}).then(() => {
                            this.editLoading = true;
                            NProgress.start();
                            let para = Object.assign({}, this.editForm);
                            para.birth = (!para.birth || para.birth == '') ? '' : util.formatDate.format(new Date(para.birth), 'yyyy-MM-dd');
                            editUser(para).then((res) => {
                                this.editLoading = false;
                                NProgress.done();
                                this.$notify({
                                    title: '成功',
                                    message: '提交成功',
                                    type: 'success'
                                });
                                this.$refs['editForm'].resetFields();
                                this.editFormVisible = false;
                                this.getUsers();
                            });
                        });
                    }
                });
            },
            //新增
            addSubmit: function () {
                this.$confirm('确认提交吗？', '提示', {}).then(() => {
                    this.addLoading = true;
                    NProgress.start();
                    let para = Object.assign({}, this.form);
                    para.birth = (!para.birth || para.birth == '') ? '' : util.formatDate.format(new Date(para.birth), 'yyyy-MM-dd');
                    addUser(para).then((res) => {
                        this.addLoading = false;
                        NProgress.done();
                        this.$notify({
                            title: '成功',
                            message: '提交成功',
                            type: 'success'
                        });
                        this.addFormVisible = false;
                        this.getUsers();
                    });
                });
            },
            selsChange: function (sels) {
                this.sels = sels;
            },
            //批量删除
            batchRemove: function () {
                var ids = this.sels.map(item => item.id).toString();
                this.$confirm('确认删除选中记录吗？', '提示', {
                    type: 'warning'
                }).then(() => {
                    this.listLoading = true;
                    NProgress.start();
                    let para = { ids: ids };
                    batchRemoveUser(para).then((res) => {
                        this.listLoading = false;
                        NProgress.done();
                        this.$notify({
                            title: '成功',
                            message: '删除成功',
                            type: 'success'
                        });
                        this.getUsers();
                    });
                }).catch(() => {

                });
            }
        },
        mounted() {
            this.getUsers();
        }
    }

</script>

<style lang="less">
	.el-dialog__body{
		padding-bottom: 0 !important;
	}

</style>