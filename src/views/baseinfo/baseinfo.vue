<template>
    <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="180">
        <FormItem label="合作社理事会人数" prop="baseDirector">
            <Input type="number" v-model="formValidate.baseDirector" placeholder="请输入人数"></Input>
        </FormItem>
        <FormItem label="关键岗位人员" prop="baseCrux">
            <Input type="number" v-model="formValidate.baseCrux" placeholder="请输入人数"></Input>
        </FormItem>
        <FormItem label="上一年雇佣人数" prop="baseHire">
            <Input type="number" v-model="formValidate.baseHire" placeholder="请输入人数"></Input>
        </FormItem>
        <FormItem label="合作社社员人数" prop="baseMembers">
            <Input type="number" v-model="formValidate.baseMembers" placeholder="请输入人数"></Input>
        </FormItem>
        <FormItem label="土地性质">
            <Row>
                <Col span="10">
                    <Input v-model="formValidate.baseNature" placeholder=""></Input>
                </Col>
                <Col span="4" style="text-align: center">带地入社，租赁</Col>
                <Col span="10">
                    <Input v-model="formValidate.baseLease" placeholder=""></Input>
                </Col>
            </Row>
        </FormItem>
        <FormItem>
            <Button type="primary" @click="handleSubmit('formValidate')">提交</Button>
            <Button type="ghost" @click="handleReset('formValidate')" style="margin-left: 8px">取消</Button>
        </FormItem>
    </Form>
</template>
<script>
    export default {
        data () {
            return {
                formValidate: {
                    name: '',
                    
                },
                ruleValidate: {
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
                    ],
                }
            }
        },
        methods: {
            handleSubmit (name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        this.$Message.success('Success!');
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
