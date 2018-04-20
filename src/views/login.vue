<style lang="less">
    @import './login.less'; 
</style>

<template>
    <div style="height:100%; paddding-top:50px;">
        <div class="reg" v-if="isShow">
            <Row type="flex" justify="center" class="code-row-bg margin-top-50" >
                <Col span="12">
                <Card>
                    <p slot="title">
                        请选择所在地区：
                    </p>
                    <al-selector v-model="res1" data-type="name" level="3"/>
                    <Input v-model="village" placeholder="请输入村" style="width: 300px; margin-top:30px;"></Input>
                    <Input v-model="regName" placeholder="请输入用户名" style="width: 300px; margin-top:30px;">
                    <span slot="prepend">
                                                        <Icon :size="16" type="person"></Icon>
                                                    </span>
                    </Input>
                    <Input type="password" v-model="regPassword" placeholder="请输入密码" style="width: 300px; margin-top:30px;">
                    <span slot="prepend">
                                                        <Icon :size="14" type="locked"></Icon>
                                                    </span>
                    </Input>
                    <Input type="password" v-model="regPassword2" placeholder="请输入密码" style="width: 300px; margin-top:30px;">
                    <span slot="prepend">
                                                        <Icon :size="14" type="locked"></Icon>
                                                    </span>
                    </Input>
                    <div>
                        <Button @click="areaSubmit"  class="margin-top-50" style="width: 100px; " type="primary" long>提交</Button>
                    </div>
                </Card>



                </Col>


            </Row>

        </div>

                <div class="login" v-if="!isShow">
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
                                    <div>
                                        <a @click="register">注册</a>
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
            form: {
                userName: '',
                password: ''
            },
            regName:'',
            regPassword:'',
            regPassword2:'',
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
        params.append("name", this.regName);
        params.append("password", this.regPassword2);

        var that = this;
        axios
          .post(global.API_PATH+"user/index", params)
          .then(response => {
            if(response.data == 'success'){
              //注册成功挑到首页
                that.isShow = false;
            }else{
              this.$Message.error('注册失败，请重新注册');
            }
          })
          .catch(error => {
            this.$Message.error(error);
          });




      },
        register () {
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
                          if(response.data != null){
                            sessionStorage.setItem("dept_id", response.data.w_dept_id);
                            this.$router.push({
                              name: 'home_index'
                            });
                          }else{
                            this.$Message.error("用户名或密码错误！");
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
