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
                    retailOwner: '',
                    retailArea: '',
                    retailId: '',
                    retailTel: '',
                    retailAddress: '',
                    retailType: '',
                    thisRetailContract:''
                },
                actionUrl:global.API_PATH+"privatemsg/img_upload",
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
                    
                ],
                thisIndex:1
            }
        },
        methods: {
            handleSubmit (name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        console.log(this.formValidate.retailType);

                        let params = new URLSearchParams();
                        params.append("private_owner", this.formValidate.retailOwner);
                        params.append("private_soil_area", this.formValidate.retailArea);
                        params.append("private_ID_num", this.formValidate.retailId);
                        params.append("private_tel_num", this.formValidate.retailTel);
                        params.append("private_address", this.formValidate.retailAddress);
                        params.append("private_soil_name", this.formValidate.retailType);
                        // params.append("private_soil_contract", this.formValidate.thisRetailContract);

                        params.append("private_dept_id", sessionStorage.getItem("dept_id"));

                   // private_dept_id、private_owner、private_soil_area、private_ID_num、private_tel_num、private_address、private_soil_name、private_soil_contract（文件）
                        axios
                            .post(global.API_PATH+"privatemsg/private_msg_insert", params)
                            .then(response => {
                                if(response.data == "success"){
                                    this.data1.push({
                                    retailIndex:this.thisIndex++,
                                    retailOwner:this.formValidate.retailOwner,
                                    retailArea: this.formValidate.retailArea,
                                    retailId: this.formValidate.retailId,
                                    retailTel: this.formValidate.retailTel,
                                    retailAddress: this.formValidate.retailAddress,
                                    retailType: this.formValidate.retailType,
                                });
                                }
                            })
                            .catch(error => {
                                this.$Message.error('错误'+error);
                            });

                            console.log(this.data1);
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
                let params = new URLSearchParams();
                params.append("private_dept_id", sessionStorage.getItem("dept_id"));
                axios
                    .post(global.API_PATH+"privatemsg/private_msg_sel", params)
                    .then(response => {
                        for(let i=0;i<response.data.length;i++){
                            this.thisIndex = i+1;
                            this.data1.push({
                                retailIndex:i+1,
                                retailOwner: response.data[i].w_private_owner,
                                retailArea: response.data[i].w_private_soil_area,
                                retailId: response.data[i].w_private_ID_num,
                                retailTel: response.data[i].w_private_tel_num,
                                retailAddress: response.data[i].w_private_address,
                                retailType: response.data[i].w_private_soil_name
                            });
                        }

                        console.log(this.data1);
                    })
                    .catch(error => {
                        this.$Message.error('错误'+error);
                    });
            }
        },
        created(){
            this.retailGet();
        }
    }
</script>


<style>

</style>


