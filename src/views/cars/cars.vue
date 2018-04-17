<template>
<div>


    <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="120">
        <Row>
            <Col span="8">
                <FormItem label="农机和经营车辆名称" prop="carsName">
                    <Input v-model="formValidate.carsName" placeholder="农机和经营车辆名称"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="单位" prop="carsUnit">
                    <Input v-model="formValidate.carsUnit" placeholder="土地面积(亩)"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="品牌型号" prop="carsType">
                    <Input v-model="formValidate.carsType" placeholder="品牌型号"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="单价（万元）" prop="carsPrice">
                    <Input v-model="formValidate.carsPrice" placeholder="单价（万元）"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="数量" prop="carsNum">
                    <Input v-model="formValidate.carsNum" placeholder="数量"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="购买金额（万元）" prop="carsSum">
                    <Input v-model="formValidate.carsSum" placeholder="购买金额（万元）"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="购买时间" prop="carsTimer">
                    <Input v-model="formValidate.carsTimer" placeholder="购买时间"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="农机补贴（万元）" prop="carsSubsidy">
                    <Input v-model="formValidate.carsSubsidy" placeholder="农机补贴（万元）"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="归属" prop="carsAscription">
                    <Select v-model="formValidate.carsAscription" placeholder="归属">
                        <Option value="0">合作社</Option>
                        <Option value="1">个人</Option>
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
    import axios from 'axios';
    export default {
        data () {
            return {
                formValidate: {
                    carsName: '',
                    carsUnit: '',
                    carsType: '',
                    carsPrice: '',
                    carsNum: '',
                    carsSum: '',
                    carsTimer:'',
                    carsSubsidy:'',
                    carsAscription:''
                },
                ruleValidate: {
                    carsName: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    carsUnit: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    carsType: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    carsPrice: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    carsNum: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    carsSum: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    carsTimer: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    carsSubsidy: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    carsAscription: [
                        { required: true, message: '必须选择一项', trigger: 'change' }
                    ]
                },
                columns1: [
                    {
                        title:"序号",
                        key:"retailIndex"
                    },
                    {
                        title: '农机和经营车辆名称',
                        key: 'carsName'
                    },
                    {
                        title: '单位',
                        key: 'carsUnit'
                    },
                    {
                        title: '品牌型号',
                        key: 'carsType'
                    },
                    {
                        title: '单价(万元)',
                        key: 'carsPrice'
                    },
                    {
                        title: '数量',
                        key: 'carsNum'
                    },
                    {
                        title: '购买金额(万元)',
                        key: 'carsSum'
                    },
                    {
                        title: '购买时间',
                        key: 'carsTimer'
                    },
                    {
                        title: '农机补贴(万元)',
                        key: 'carsSubsidy'
                    },
                    {
                        title: '归属',
                        key: 'carsAscription'
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
                        this.carsAdd();
                    } else {
                        this.$Message.error('Fail!');
                    }
                })
            },
            handleReset (name) {
                this.$refs[name].resetFields();
            },
            //信息提交
            carsAdd(){
                console.log(this.formValidate);
                let thisObj = {
                    machine_name:this.formValidate.carsName,
                    machine_brand:this.formValidate.carsType,
                    machine_sell_price:this.formValidate.carsPrice,
                    machine_num:this.formValidate.carsNum,
                    machine_buy_price:this.formValidate.carsSum,
                    machine_buy_time:this.formValidate.carsTimer,
                    machine_allowance:this.formValidate.carsSubsidy,
                    machine_owner:this.formValidate.carsAscription,
                    dept_id:'20'
                }
                // let params = new URLSearchParams();
                // params.append("machine_name", this.formValidate.carsName);
                // params.append("machine_brand", this.formValidate.carsType);
                // params.append("machine_sell_price", formValidate.carsPrice);
                // params.append("machine_num", this.formValidate.carsNum);
                // params.append("machine_buy_price", this.formValidate.carsSum);
                // params.append("machine_buy_time", this.formValidate.carsTimer);
                // params.append("machine_allowance", this.formValidate.carsSubsidy);
                // params.append("machine_owner", this.formValidate.carsAscription);
                // params.append("dept_id", '20');

                axios
                    .get(global.API_PATH+"machine/machine_msg_insert",{"thisObj":"123"})
                    .then(response => {

                        let thisCarsType="合作社";
                        if(this.formValidate.carsAscription=="1"){
                            thisCarsType="个人";
                        }
                        this.data1.push({
                            carsName: this.formValidate.carsName,
                            carsUnit: this.formValidate.carsUnit,
                            carsType: this.formValidate.carsType,
                            carsPrice: this.formValidate.carsPrice,
                            carsNum: this.formValidate.carsNum,
                            carsSum: this.formValidate.carsSum,
                            carsTimer: this.formValidate.carsTimer,
                            carsSubsidy: this.formValidate.carsSubsidy,
                            carsAscription: thisCarsType
                        });
                    })
                    .catch(error => {
                        
                        this.$Message.error(error);
                    });
                    
            },
            carsGet(){
                let params = new URLSearchParams();
                //params.append("dept_id", sessionStorage.getItem("dept_id"));
                params.append("dept_id", '20');

               // var that = this;
                axios
                    .post(global.API_PATH+"machine/machine_msg_sel", params)
                    .then(response => {
                        for(val in response){
                            console.log(val);
                        }
                        let thisCarsType="合作社";
                        if(this.formValidate.carsAscription=="1"){
                            thisCarsType="个人";
                        }
                        this.data1.push({
                            carsName: this.formValidate.carsName,
                            carsUnit: this.formValidate.carsUnit,
                            carsType: this.formValidate.carsType,
                            carsPrice: this.formValidate.carsPrice,
                            carsNum: this.formValidate.carsNum,
                            carsSum: this.formValidate.carsSum,
                            carsTimer: this.formValidate.carsTimer,
                            carsSubsidy: this.formValidate.carsSubsidy,
                            carsAscription: thisCarsType
                        });
                    })
                    .catch(error => {
                        this.$Message.error('错误'+error);
                    });
            }
        },
        created(){
            this.carsGet();
        }
    }
</script>


<style>

</style>


