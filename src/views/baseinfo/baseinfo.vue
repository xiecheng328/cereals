<template>
    <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="180">
        <FormItem label="合作社名称" prop="baseName">
            <Input v-model="formValidate.baseName" placeholder="请输入合作社名称"></Input>
        </FormItem>
        <FormItem label="合作社法人" prop="basePerson">
            <Input v-model="formValidate.basePerson" placeholder="请输入法人"></Input>
        </FormItem>
        <FormItem label="合作社理事会人数" prop="baseDirector">
            <Input v-model="formValidate.baseDirector" placeholder="请输入人数"></Input>
        </FormItem>
        <FormItem label="关键岗位人员" prop="baseCrux">
            <Input v-model="formValidate.baseCrux" placeholder="请输入人数"></Input>
        </FormItem>
        <FormItem label="上一年雇佣人数" prop="baseHire">
            <Input v-model="formValidate.baseHire" placeholder="请输入人数"></Input>
        </FormItem>
        <FormItem label="合作社社员人数" prop="baseMembers">
            <Input v-model="formValidate.baseMembers" placeholder="请输入人数"></Input>
        </FormItem>
        <FormItem label="土地性质">
            <Input v-model="formValidate.baseNature" placeholder=""></Input>
        </FormItem>
        <FormItem label="土地总面积">
            <span v-text="total"></span>
        </FormItem>
        <FormItem>
            <Button type="primary" @click="handleSubmit('formValidate')">提交</Button>
            <Button type="ghost" @click="handleReset('formValidate')" style="margin-left: 8px">取消</Button>
        </FormItem>
    </Form>
</template>
<script>
    import axios from 'axios';
    export default {
        data () {
            return {
                formValidate: {
                    baseDirector: ''
                },
                total:0,
                ruleValidate: {
                    baseName: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    basePerson: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    baseDirector: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    baseCrux: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    baseHire: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    baseMembers: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ]
                }
            }
        },
        created(){
            let params = new URLSearchParams();
            params.append("dept_id", sessionStorage.getItem("dept_id"));
            axios
                .post(global.API_PATH+"coop/get_coop_all_msg", params)
                .then(response => {
                    if(response.data){
                        this.formValidate.baseName = response.data.w_coop_name;
                        this.formValidate.basePerson = response.data.w_coop_person;
                        this.formValidate.baseDirector = response.data.w_coop_directors_num;
                        this.formValidate.baseCrux = response.data.w_coop_keyjob_num;
                        this.formValidate.baseHire = response.data.w_coop_pyear_employ_num;
                        this.formValidate.baseMembers = response.data.w_coop_member_num;
                        this.formValidate.baseNature = response.data.w_coop_soil_property;
                        this.total = response.data.total;
                    }
                    
                })
                .catch(error => {
                    console.log(error);
                    this.$Message.error(error);
                });
        },
        methods: {
            //提交按钮
            handleSubmit (name) {
                let params = new URLSearchParams();
                params.append("name", this.formValidate.baseName);
                params.append("person", this.formValidate.basePerson);
                params.append("directors_num", this.formValidate.baseDirector);
                params.append("keyjob_num", this.formValidate.baseCrux);
                params.append("pyear_employ_num", this.formValidate.baseHire);
                params.append("member_num", this.formValidate.baseMembers);
                params.append("soil_property", this.formValidate.baseNature);
                params.append("dept_id", sessionStorage.getItem("dept_id"));

                axios
                    .post(global.API_PATH+"coop/coop_all_msg_insert",params)
                    .then(response => {
                       this.$router.push({
                           name:'testpage'
                       })
                    })
                    .catch(error => {

                        this.$Message.error(error);
                    });


//                this.$refs[name].validate((valid) => {
//                    if (valid) {
//                        this.$Message.success('Success!');
//                    } else {
//                        this.$Message.error('Fail!');
//                    }
//                })
            },
            //取消操作
            handleReset (name) {
                this.$refs[name].resetFields();
            }
           
        }
    }
</script>
<style>

</style>

