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
            console.log(this.showRes);

            // axios.post(global.API_PATH+"user/index",,function(){
              //  country=xxx &town=xxx&province=xxx
            // });

            let params = new URLSearchParams();
            params.append("country", this.showRes[0]);
            params.append("town", this.showRes[1]);
            params.append("province", this.showRes[2]);
            params.append("village", this.village);

            console.log(params);
            var that = this;
            axios
                .post(global.API_PATH+"user/index", params)
                .then(response => {

                    if(response.data.isReg){
                        //去注册
                        this.isCheck = false;
                        this.whichName = 'name2';
                    }else{
                        //去登陆
                        this.isCheck = false;
                        this.whichName = 'name1';
                    }
                    // this.$Message.success("注册成功");
                    console.log(response);
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
                    this.$store.commit('setAvator', 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3448484253,3685836170&fm=27&gp=0.jpg');
                    if (this.form.userName === 'iview_admin') {
                        Cookies.set('access', 0);
                    } else {
                        Cookies.set('access', 1);
                    }
                    this.$router.push({
                        name: 'home_index'
                    });
                }
            });
        },
        handleReg () {
            console.log(this.regForm);
            axios
                .post(global.API_PATH+"user/index", params)
                .then(response => {

                    if(response.data.isReg){
                        //注册成功存入sessionStorage
                        sessionStorage.setItem("user", "value");
                    }else{
                        this.$Message.error(response);
                    }
                })
                .catch(error => {
                    this.$Message.error(error);
                });
            this.$router.push({
                name: 'home_index'
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
