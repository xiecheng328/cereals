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
                        <Option value="土地确权证">土地确权证</Option>
                        <Option value="土地承包合同">土地承包合同</Option>
                        <Option value="村里台账信息">村里台账信息</Option>
                    </Select>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <Upload :action="actionUrl" name="file">
                    <Button type="ghost" icon="ios-cloud-upload-outline">Upload files</Button>
                </Upload>
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
    import axios from 'axios';
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
                    
                ],
                actionUrl:global.API_PATH+"coop/img_upload",
                thisIndex:1
            }
        },
        created(){
//            coopName: '',
//                coopArea: '',
//                coopTel: '',
//                coopId: '',
//                coopAddress: '',
//                coopOwnre: '',
//                coopOTel: '',
//                coopOAddress: '',
//                coopType:''
            let params = new URLSearchParams();
            params.append("dept_id", sessionStorage.getItem("dept_id"));
            axios
                .post(global.API_PATH+"coop/coop_msg_sel",params)
                .then(response => {
                    for(var i=0;i<response.data.length;i++){
                        this.thisIndex = i+1;
                        var o = new Object();
                        o.coopIndex = i+1;
                        o.coopName = response.data[i].w_coop_grantor;
                        o.coopArea = response.data[i].w_coop_soil_area;
                        o.coopTel = response.data[i].w_coop_tel_num;
                        o.coopId = response.data[i].w_coop_ID_num;
                        o.coopAddress = response.data[i].w_coop_address;
                        o.coopOwnre = response.data[i].w_coop_soil_owner;
                        o.coopOTel = response.data[i].w_coop_soil_tel_num;
                        o.coopOAddress = response.data[i].w_coop_soil_address;
                        o.coopType = response.data[i].w_coop_soil_name;
                        this.data1.push(o);
                    }
                }).catch(error => {
                    this.$Message.error(error);
                });
        },
        methods: {
            handleSubmit (name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        let params = new URLSearchParams();
                        params.append("grantor", this.formValidate.coopName);
                        params.append("area", this.formValidate.coopArea);
                        params.append("id_num", this.formValidate.coopId);
                        params.append("tel_num", this.formValidate.coopTel);
                        params.append("address", this.formValidate.coopAddress);
                        params.append("owner", this.formValidate.coopOTel);
                        params.append("soil_tel_num", this.formValidate.coopOwnre);
                        params.append("soil_address", this.formValidate.coopOAddress);
                        params.append("soil_name", this.formValidate.coopType);
                        params.append("dept_id", sessionStorage.getItem("dept_id"));
                        axios
                            .post(global.API_PATH+"coop/coop_msg_insert",params)
                            .then(response => {
                                this.data1.push({
                                    coopIndex:++this.thisIndex,
                                    coopName: this.formValidate.coopName,
                                    coopArea: this.formValidate.coopArea,
                                    coopTel: this.formValidate.coopTel,
                                    coopId: this.formValidate.coopId,
                                    coopAddress: this.formValidate.coopAddress,
                                    coopOTel: this.formValidate.coopOTel,
                                    coopOwnre: this.formValidate.coopOwnre,
                                    coopOAddress: this.formValidate.coopOAddress,
                                    coopType:this.formValidate.coopType
                                });
                            })
                            .catch(error => {
                                this.$Message.error(error);
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


