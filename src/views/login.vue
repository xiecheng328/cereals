<style lang="less">
    @import './login.less'; 
</style>

<template>
    <div style="height:100%; paddding-top:50px;">
        
                <div v-if="isCheck">
                    <Row type="flex" justify="center" class="code-row-bg margin-top-50" >
                        <Col span="12">
                            <Card>
                                <p slot="title">
                                    请选择所在地区：
                                </p>
                                <al-selector v-model="res1" data-type="name" level="3"/>
                                 <Input v-model="village" placeholder="请输入村" style="width: 300px; margin-top:30px;"></Input>
                                 <div>
                                    <Button @click="areaSubmit"  class="margin-top-50" style="width: 100px; " type="primary" long>提交</Button>
                                 </div>
                            </Card>
                            
                        </Col>
            
                    </Row>
                </div>
                

                <div class="login" v-if="isShow">
                    <div class="login-con">

                        <Card :bordered="false">

                            <Tabs :value="whichName">
                                <TabPane label="登录" name="name1">
                                    
                                    <div class="form-con">
                                        <Form ref="loginForm" :model="form" :rules="rules">
                                            <FormItem prop="userName">
                                                <Input v-model="form.userName" placeholder="请输入用户名">
                                                    <span slot="prepend">
                                                        <Icon :size="16" type="person"></Icon>
                                                    </span>
                                                </Input>
                                            </FormItem>
                                            <FormItem prop="password">
                                                <Input type="password" v-model="form.password" placeholder="请输入密码">
                                                    <span slot="prepend">
                                                        <Icon :size="14" type="locked"></Icon>
                                                    </span>
                                                </Input>
                                            </FormItem>
                                            <FormItem>
                                                <Button @click="handleSubmit" type="primary" long>登录</Button>
                                            </FormItem>
                                        
                                        </Form>
                                    </div>
                                    
                                </TabPane>
                                <TabPane label="注册" name="name2">

                                    <div class="form-con">
                                        <Form ref="registerForm" :model="regForm" :rules="regRules">
                                            <FormItem prop="regName">
                                                <Input v-model="regForm.regName" placeholder="请输入用户名">
                                                    <span slot="prepend">
                                                        <Icon :size="16" type="person"></Icon>
                                                    </span>
                                                </Input>
                                            </FormItem>
                                            <FormItem prop="regPassword">
                                                <Input type="password" v-model="regForm.regPassword" placeholder="请输入密码">
                                                    <span slot="prepend">
                                                        <Icon :size="14" type="locked"></Icon>
                                                    </span>
                                                </Input>
                                            </FormItem>
                                            <FormItem>
                                                <Button @click="handleReg" type="primary" long>注册</Button>
                                            </FormItem>
                                        </Form>
                                    </div>
                                </TabPane>
                            </Tabs>
                                    
                        
                        </Card>
                    </div>
                </div>    
    </div>
    
</template>

<script>
import Cookies from 'js-cookie';
import Vue from 'vue';
import iviewArea from 'iview-area';
import axios from 'axios';
Vue.use(iviewArea);


export default {
    data () {
        return {
            isShow:false,
            isCheck:true,
            form: {
                userName: '',
                password: ''
            },
            regForm:{
                regName:'',
                regPassword:''
            },
            rules: {
                userName: [
                    { required: true, message: '账号不能为空', trigger: 'blur' }
                ],
                password: [
                    { required: true, message: '密码不能为空', trigger: 'blur' }
                ],
                
            },
            regRules:{
                regName: [
                    { required: true, message: '账号不能为空', trigger: 'blur' }
                ],
                regPassword: [
                    { required: true, message: '密码不能为空', trigger: 'blur' }
                ]
            },
            res1: [],
            ex: ['河北省', '张家口市', '怀来县'],
            village:'',
            showRes: [],
            whichName:'name1'
        };
    },
    methods: {
        areaSubmit () {

           let params = new URLSearchParams();
            params.append("province", this.showRes[0]);
            params.append("city", this.showRes[1]);
            params.append("country", this.showRes[2]);
            params.append("town", this.showRes[3]);
            params.append("village", this.village);

            console.log(params);
            var that = this;
            axios
                .post(global.API_PATH+"user/index", params)
                .then(response => {
                    sessionStorage.setItem("dept_id", response.data.w_dept_id);
                    if(response.data.isReg){
                        //去注册
                        this.isCheck = false;
                        this.whichName = 'name2';
                    }else{
                        //去登陆
                        this.isCheck = false;
                        this.whichName = 'name1';
                    }
                })
                .catch(error => {
                    this.$Message.error(error);
                });

            this.isShow = true;

            

        },
        handleSubmit () {   
            this.$refs.loginForm.validate((valid) => {
                if (valid) {
                    Cookies.set('user', this.form.userName);
                    Cookies.set('password', this.form.password);

                    let params = new URLSearchParams();
                    params.append("name", this.form.userName);
                    params.append("pass", this.form.password);
                    params.append("dept_id", sessionStorage.getItem("dept_id"));

                    axios
                        .post(global.API_PATH+"user/login", params)
                        .then(response => {

                            if(response.data == "success"){
                                //登录成功存入sessionStorage
                                this.$router.push({
                                    name: 'home_index'
                                });
                            }else{
                                this.$Message.error("错误！");
                            }
                        });
                }
            });
        },
        handleReg () {
            this.$refs.registerForm.validate((valid) => {
                if (valid) {
                    Cookies.set('user', this.regForm.regName);
                    Cookies.set('password', this.regForm.regPassword);

                    let params = new URLSearchParams();
                    params.append("name", this.regForm.regName);
                    params.append("pass", this.regForm.regPassword);
                    params.append("dept_id", sessionStorage.getItem("dept_id"));
                    axios
                        .post(global.API_PATH+"user/reg", params)
                        .then(response => {
                            if(response.data == "success"){
                                //注册成功挑到首页
                                this.$router.push({
                                    name: 'home_index'
                                });
                            }else{
                                this.$Message.error(response);
                            }
                        });
                }
            });
            
        },
        renderFormat (label) {
            return label.join(' => ');
        }
    },
    watch: {
        res1 (val) {
            this.showRes = val;
        },
        resDefault (val) {
            this.showRes = val;
        }
    }
};
</script>

<style>
    .login-con {
        top: 50%;
        left: 50%;
        transform: translateY(-60%) translatex(-50%);
    }
    .margin-top-50{
        margin-top:50px;
    }
</style>
