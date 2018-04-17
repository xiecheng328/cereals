<template>
<div>


    <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="120">
        <Row>
            <Col span="8">
                <FormItem label="实际种植人" prop="coopName">
                    <Input v-model="formValidate.coopName" placeholder="实际种植人"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="土地面积(亩)" prop="coopArea">
                    <Input v-model="formValidate.coopArea" placeholder="土地面积(亩)"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="身份证号" prop="coopId">
                    <Input v-model="formValidate.coopId" placeholder="身份证号"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="联系电话" prop="coopTel">
                    <Input v-model="formValidate.coopTel" placeholder="联系电话"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="联系地址" prop="coopAddress">
                    <Input v-model="formValidate.coopAddress" placeholder="联系地址"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="土地所有人" prop="coopOwnre">
                    <Input v-model="formValidate.coopOwnre" placeholder="土地所有人"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="联系电话" prop="coopOTel">
                    <Input v-model="formValidate.coopOTel" placeholder="联系电话"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="联系地址" prop="coopOAddress">
                    <Input v-model="formValidate.coopOAddress" placeholder="联系地址"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="合作方式" prop="coopType">
                    <Select v-model="formValidate.coopType" placeholder="必须三选一">
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
                    coopName: '',
                    coopArea: '',
                    coopTel: '',
                    coopId: '',
                    coopAddress: '',
                    coopOwnre: '',
                    coopOTel: '',
                    coopOAddress: '',
                    coopType:''
                },
                ruleValidate: {
                    coopName: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    coopArea: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    coopTel: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    coopId: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    coopOAddress: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    coopOwnre: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    coopOTel: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    coopAddress: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    coopType: [
                        { required: true, message: '必须选择一项', trigger: 'change' }
                    ]
                },
                columns1: [
                    {
                        title: '序号',
                        key: 'coopIndex'
                    },
                    {
                        title: '实际种植人',
                        key: 'coopName'
                    },
                    {
                        title: '土地面积（亩）',
                        key: 'coopArea'
                    },
                    {
                        title: '身份证',
                        key: 'coopId'
                    },
                    {
                        title: '联系电话',
                        key: 'coopTel'
                    },
                    {
                        title: '联系地址',
                        key: 'coopAddress'
                    },
                    {
                        title: '土地所有人',
                        key: 'coopOwnre'
                    },
                    {
                        title: '联系电话',
                        key: 'coopOTel'
                    },
                    {
                        title: '联系地址',
                        key: 'coopOAddress'
                    },
                    {
                        title: '合作方式',
                        key: 'coopType'
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
                        let thisCoopType="土地确权证";
                        if(this.formValidate.coopType=="1"){
                            thisCoopType="土地承包合同";
                        }else if(this.formValidate.coopType=="2"){
                            thisCoopType="村里台账信息";
                        }
                        this.data1.push({
                            coopName: this.formValidate.coopName,
                            coopArea: this.formValidate.coopArea,
                            coopTel: this.formValidate.coopTel,
                            coopId: this.formValidate.coopId,
                            coopAddress: this.formValidate.coopAddress,
                            coopOTel: this.formValidate.coopOTel,
                            coopOwnre: this.formValidate.coopOwnre,
                            coopOAddress: this.formValidate.coopOAddress,
                            coopType:thisCoopType
                        });
                    } else {
                        this.$Message.error('Fail!');
                    }
                })
            },
            handleReset (name) {
                this.$refs[name].resetFields();
            }
        }
    }
</script>


<style>

</style>


