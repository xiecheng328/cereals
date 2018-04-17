<template>
<div>


    <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="120">
        <Row>
            <Col span="8">
                <FormItem label="土地所有人" prop="retailOwner">
                    <Input v-model="formValidate.retailOwner" placeholder="土地所有人"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="土地面积(亩)" prop="retailArea">
                    <Input v-model="formValidate.retailArea" placeholder="土地面积(亩)"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="身份证号" prop="retailId">
                    <Input v-model="formValidate.retailId" placeholder="身份证号"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="联系电话" prop="retailTel">
                    <Input v-model="formValidate.retailTel" placeholder="联系电话"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="联系地址" prop="retailAddress">
                    <Input v-model="formValidate.retailAddress" placeholder="联系地址"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="合作方式" prop="retailType">
                    <Select v-model="formValidate.retailType" placeholder="必须三选一">
                        <Option value="0">土地确权证</Option>
                        <Option value="1">土地承包合同</Option>
                        <Option value="2">村里台账信息</Option>
                    </Select>
                </FormItem>
            </Col>
        </Row>
        <FormItem>
            <Button type="primary" @click="handleSubmit('formValidate')">添加</Button>
            <Button type="ghost" @click="handleReset('formValidate')" style="margin-left: 8px">取消</Button>
        </FormItem>
    </Form>
<Table border :columns="columns1" :data="data1"></Table>
 </div>   
</template>
<script>
    export default {
        data () {
            return {
                formValidate: {
                    retailOwner: '',
                    retailArea: '',
                    retailId: '',
                    retailTel: '',
                    retailAddress: '',
                    retailType: '',
                },
                ruleValidate: {
                    retailOwner: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    retailArea: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    retailId: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    retailTel: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    retailAddress: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    retailType: [
                        { required: true, message: '必须选择一项', trigger: 'change' }
                    ]
                },
                columns1: [
                    {
                        title:"序号",
                        key:"retailIndex"
                    },
                    {
                        title: '土地所有人',
                        key: 'retailOwner'
                    },
                    {
                        title: '土地面积（亩）',
                        key: 'retailArea'
                    },
                    {
                        title: '身份证',
                        key: 'retailId'
                    },
                    {
                        title: '联系电话',
                        key: 'retailTel'
                    },
                    {
                        title: '联系地址',
                        key: 'retailAddress'
                    },
                    {
                        title: '合作方式',
                        key: 'retailType'
                    }
                ],
                data1: [
                    
                ]
            }
        },
        methods: {
            handleSubmit (name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        let thisRetailType="土地确权证";
                        if(this.formValidate.retailType=="1"){
                            thisRetailType="土地承包合同";
                        }else if(this.formValidate.retailType=="2"){
                            thisRetailType="村里台账信息";
                        }
                        this.data1.push({
                            retailOwner: this.formValidate.retailOwner,
                            retailArea: this.formValidate.retailArea,
                            retailId: this.formValidate.retailId,
                            retailTel: this.formValidate.retailTel,
                            retailAddress: this.formValidate.retailAddress,
                            retailType: thisRetailType
                        });
                    } else {
                        this.$Message.error('Fail!');
                    }
                })
            },
            handleReset (name) {
                this.$refs[name].resetFields();
            },
            //获取列表
            retailGet(){

            }
        },
        created(){

        }
    }
</script>


<style>

</style>


