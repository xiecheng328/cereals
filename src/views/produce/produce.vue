<template>
<div>


    <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="120">
        <Row>
            <Col span="8">
                <FormItem label="品类" prop="produceCategory">
                    <Input v-model="formValidate.produceCategory" placeholder="品类"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="土地(托管流转)" prop="produceEarth">
                    <Input v-model="formValidate.produceEarth" placeholder="土地(托管流转)"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="种子" prop="produceSeed">
                    <Input v-model="formValidate.produceSeed" placeholder="种子"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="化肥" prop="produceFertilizer">
                    <Input v-model="formValidate.produceFertilizer" placeholder="化肥"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="农药" prop="producePesticides">
                    <Input v-model="formValidate.producePesticides" placeholder="农药"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="播种" prop="produceSow">
                    <Input v-model="formValidate.produceSow" placeholder="播种"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="旋耕" prop="produceCultivation">
                    <Input v-model="formValidate.produceCultivation" placeholder="旋耕"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="喷施" prop="produceSpray">
                    <Input v-model="formValidate.produceSpray" placeholder="喷施"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="收割(直收、脱粒)" prop="produceHarvest">
                    <Input v-model="formValidate.produceHarvest" placeholder="收割(直收、脱粒)"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="秋整地" prop="producePrepare">
                    <Input v-model="formValidate.producePrepare" placeholder="秋整地"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="人工" prop="producePerson">
                    <Input v-model="formValidate.producePerson" placeholder="人工"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="保险" prop="produceInsurance">
                    <Input v-model="formValidate.produceInsurance" placeholder="保险"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="利息" prop="produceInterest">
                    <Input v-model="formValidate.produceInterest" placeholder="利息"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="种植成本" prop="produceCost">
                    <Input v-model="formValidate.produceCost" placeholder="种植成本"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="预计产出(亩/斤)" prop="produceExpect">
                    <Input v-model="formValidate.produceExpect" placeholder="预计产出(亩/斤)"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="预计(等级/水分)" prop="produceEstimate">
                    <Input v-model="formValidate.produceEstimate" placeholder="预计(等级/水分)"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="种植补贴(粮补、地补)" prop="producePlantSubsidy">
                    <Input v-model="formValidate.producePlantSubsidy" placeholder="种植补贴(粮补、地补)"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="政策补贴(生产、调茬)" prop="producePolicySubsidy">
                    <Input v-model="formValidate.producePolicySubsidy" placeholder="政策补贴(生产、调茬)"></Input>
                </FormItem>
            </Col>
        </Row>
        <Row>
            <Col span="8">
                <FormItem label="预计收益" prop="produceProfit">
                    <Input v-model="formValidate.produceProfit" placeholder="预计收益"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="其他费用" prop="produceOther">
                    <Input v-model="formValidate.produceOther" placeholder="其他费用"></Input>
                </FormItem>
            </Col>
            <Col span="8">
                <FormItem label="备注" prop="produceRemarks">
                    <Input v-model="formValidate.produceRemarks" placeholder="备注"></Input>
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
                    produceCategory:'',
                    produceEarth:'',
                    produceSeed:'',
                    produceFertilizer:'',
                    producePesticides:'',
                    produceSow:'',
                    produceCultivation:'',
                    produceSpray:'',
                    produceHarvest:'',
                    producePrepare:'',
                    producePerson:'',
                    produceInsurance:'',
                    produceInterest:'',
                    produceCost:'',
                    produceExpect:'',
                    produceEstimate:'',
                    producePlantSubsidy:'',
                    producePolicySubsidy:'',
                    produceProfit:'',
                    produceOther:'',
                    produceRemarks:''
                },
                ruleValidate: {
                    produceCategory: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceEarth: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceSeed: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceFertilizer: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    producePesticides: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceSow: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceCultivation: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceSpray: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceHarvest: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    producePrepare: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    producePerson: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceInsurance: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceInterest: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceCost: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceExpect: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceEstimate: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    producePlantSubsidy: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    producePolicySubsidy: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceProfit: [
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceOther:[
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                    produceRemarks:[
                        { required: true, message: '此项不能为空', trigger: 'blur' }
                    ],
                },
                columns1: [
                    {
                        title:"序号",
                        key:"produceIndex"
                    },
                    {
                        title: '品类',
                        key: 'produceCategory'
                    },
                    {
                        title: '土地（托管、流转）',
                        key: 'produceEarth'
                    },
                    {
                        title: '种子',
                        key: 'produceSeed'
                    },
                    {
                        title: '化肥',
                        key: 'produceFertilizer'
                    },
                    {
                        title: '农药',
                        key: 'producePesticides'
                    },
                    {
                        title: '播种',
                        key: 'produceSow'
                    },
                    {
                        title: '旋耕',
                        key: 'produceCultivation'
                    },
                    {
                        title: '喷施',
                        key: 'produceSpray'
                    },
                    {
                        title: '收割（直收、脱粒）',
                        key: 'produceHarvest'
                    },
                    {
                        title: '秋整地',
                        key: 'producePrepare'
                    },
                    {
                        title: '人工',
                        key: 'producePerson'
                    },
                    {
                        title: '保险',
                        key: 'produceInsurance'
                    },
                    {
                        title: '利息',
                        key: 'produceInterest'
                    },
                    {
                        title: '种植成本合计',
                        key: 'produceCost'
                    },
                    {
                        title: '预计产出（亩/斤）',
                        key: 'produceExpect'
                    },
                    {
                        title: '预计（等级/水分）',
                        key: 'produceEstimate'
                    },
                    {
                        title: '种植补贴（粮补、地补）',
                        key: 'producePlantSubsidy'
                    },
                    {
                        title: '政策补贴（生产、调茬）',
                        key: 'producePolicySubsidy'
                    },
                    {
                        title: '预期收益',
                        key: 'produceProfit'
                    },
                    {
                        title: '其他费用',
                        key: 'produceOther'
                    },{
                        title:'备注',
                        key:'produceRemarks'
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
                            retailOwner: this.formValidate.retailOwner,
                            retailArea: this.formValidate.retailArea,
                            retailId: this.formValidate.retailId,
                            retailTel: this.formValidate.retailTel,
                            retailAddress: this.formValidate.retailAddress,
                            retailType: thisCoopType
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


