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
                <FormItem label="购买时间">
                    <DatePicker type="date" format='yyyy-MM-dd' v-model="formValidate.carsTimer" placeholder="购买时间" style="width: 200px"></DatePicker>
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
                        key:"carsIndex"
                    },
                    {
                        title: '农机和经营车辆名称',
                        key: 'carsName'
                    },
                    // {
                    //     title: '单位',
                    //     key: 'carsUnit'
                    // },
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
                    
                ],
                thisIndex:1
            }
        },
        
        methods: {
            changeTime(thisDate){
                let timer = new Date(thisDate);
                let timeStr = timer.getFullYear()+"-"+(timer.getMonth()+1)+"-"+timer.getDate();
                return timeStr;
            },
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
                let params = new URLSearchParams();
                params.append("machine_name", this.formValidate.carsName);
                params.append("machine_brand", this.formValidate.carsType);
                params.append("machine_sell_price", this.formValidate.carsPrice);
                params.append("machine_num", this.formValidate.carsNum);
                params.append("machine_buy_price", this.formValidate.carsSum);
                params.append("machine_buy_time", this.changeTime(this.formValidate.carsTimer));
                params.append("machine_allowance", this.formValidate.carsSubsidy);
                params.append("machine_owner", this.formValidate.carsAscription);
                params.append("dept_id", sessionStorage.getItem("dept_id"));

                axios
                    .post(global.API_PATH+"machine/machine_msg_insert",params)
                    .then(response => {

                        let thisCarsType="合作社";
                        if(this.formValidate.carsAscription=="1"){
                            thisCarsType="个人";
                        }
                        this.data1.push({
                            carsIndex:++this.thisIndex,
                            carsName: this.formValidate.carsName,
                            carsUnit: this.formValidate.carsUnit,
                            carsType: this.formValidate.carsType,
                            carsPrice: this.formValidate.carsPrice,
                            carsNum: this.formValidate.carsNum,
                            carsSum: this.formValidate.carsSum,
                            carsTimer: this.changeTime(this.formValidate.carsTimer),
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
                params.append("dept_id", sessionStorage.getItem("dept_id"));

                axios
                    .post(global.API_PATH+"machine/machine_msg_sel", params)
                    .then(response => {
                        for(let i=0;i<response.data.length;i++){
                            this.thisIndex = i+1;
                            let thisCarsType="合作社";
                            if(response.data[i].w_machine_owner=="1"){
                                thisCarsType="个人";
                            }
                            this.data1.push({
                                carsIndex:i+1,
                                carsName: response.data[i].w_machine_name,
                                carsType: response.data[i].w_machine_brand,
                                carsPrice: response.data[i].w_machine_sell_price,
                                carsNum: response.data[i].w_machine_num,
                                carsSum: response.data[i].w_machine_buy_price,
                                carsTimer: response.data[i].w_machine_buy_time,
                                carsSubsidy: response.data[i].w_machine_allowance,
                                carsAscription: thisCarsType
                            });
                        }
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


