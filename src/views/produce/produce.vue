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
<Table width="1090" border :columns="columns1" :data="data1"></Table>
 </div>   
</template>
<script>
import axios from 'axios';
    export default {
        data () {
            return {
                formValidate: {
                    produceIndex:'',
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
                        key:"produceIndex",
                        width: 100,
                        fixed: 'left'
                    },
                    {
                        title: '品类',
                        key: 'produceCategory',
                        width: 100,
                    },
                    {
                        title: '土地（托管、流转）',
                        key: 'produceEarth',
                        width: 150,
                    },
                    {
                        title: '种子',
                        key: 'produceSeed',
                        width: 100,
                    },
                    {
                        title: '化肥',
                        key: 'produceFertilizer',
                        width: 100,
                    },
                    {
                        title: '农药',
                        key: 'producePesticides',
                        width: 100,
                    },
                    {
                        title: '播种',
                        key: 'produceSow',
                        width: 100,
                    },
                    {
                        title: '旋耕',
                        key: 'produceCultivation',
                        width: 100,
                    },
                    {
                        title: '喷施',
                        key: 'produceSpray',
                        width: 100,
                    },
                    {
                        title: '收割（直收、脱粒）',
                        key: 'produceHarvest',
                        width: 150,
                    },
                    {
                        title: '秋整地',
                        key: 'producePrepare',
                        width: 100,
                    },
                    {
                        title: '人工',
                        key: 'producePerson',
                        width: 100,
                    },
                    {
                        title: '保险',
                        key: 'produceInsurance',
                        width: 100,
                    },
                    {
                        title: '利息',
                        key: 'produceInterest',
                        width: 100,
                    },
                    {
                        title: '种植成本合计',
                        key: 'produceCost',
                        width: 150,
                    },
                    {
                        title: '预计产出（亩/斤）',
                        key: 'produceExpect',
                        width: 150,
                    },
                    {
                        title: '预计（等级/水分）',
                        key: 'produceEstimate',
                        width: 150,
                    },
                    {
                        title: '种植补贴（粮补、地补）',
                        key: 'producePlantSubsidy',
                        width: 150,
                    },
                    {
                        title: '政策补贴（生产、调茬）',
                        key: 'producePolicySubsidy',
                        width: 150,
                    },
                    {
                        title: '预期收益',
                        key: 'produceProfit',
                        width: 100,
                    },
                    {
                        title: '其他费用',
                        key: 'produceOther',
                        width: 100,
                    },{
                        title:'备注',
                        key:'produceRemarks',
                        width: 100,
                    }
                ],
                data1: [
                    
                ],
                index:1
            }
        },
        methods: {
            handleSubmit (name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        this.addProduce();
                    } else {
                        this.$Message.error('Fail!');
                    }
                })
            },
            handleReset (name) {
                this.$refs[name].resetFields();
            },
            addProduce(){
                let params = new URLSearchParams();
                params.append("produfactors_dept_id", sessionStorage.getItem("dept_id"));
                params.append("produfactors_cate", this.formValidate.produceCategory);
                params.append("produfactors_soil_cate", this.formValidate.produceEarth);
                params.append("produfactors_seed_price", this.formValidate.produceSeed);
                params.append("produfactors_chem_price", this.formValidate.produceFertilizer);
                params.append("produfactors_pesticide_price", this.formValidate.producePesticides);
                params.append("produfactors_sowing_price", this.formValidate.produceSow);
                params.append("produfactors_rotary_price", this.formValidate.produceCultivation);
                params.append("produfactors_spraying_price", this.formValidate.produceSpray);
                params.append("produfactors_harvest_price", this.formValidate.produceHarvest);
                params.append("produfactors_autusoil_price", this.formValidate.producePrepare);
                params.append("produfactors_manmade_price", this.formValidate.producePerson);
                params.append("produfactors_insurance_price", this.formValidate.produceInsurance);
                params.append("produfactors_accrual_price", this.formValidate.produceInterest);
                params.append("produfactors_plantcost_sum", this.formValidate.produceCost);
                params.append("produfactors_yield_num", this.formValidate.produceExpect);
                params.append("produfactors_dew", this.formValidate.produceEstimate);
                params.append("produfactors_plant_allowance", this.formValidate.producePlantSubsidy);
                params.append("produfactors_grov_allowance", this.formValidate.producePolicySubsidy);
                params.append("produfactors_pearning", this.formValidate.produceProfit);
                params.append("produfactors_other_price", this.formValidate.produceOther);
                params.append("produfactors_remark", this.formValidate.produceRemarks);

                axios
                    .post(global.API_PATH+"produfactors/produfactors_msg_insert",params)
                    .then(response => {

                        this.data1.push({
                            produceIndex:this.index++,
                            produceCategory:this.formValidate.produceCategory,
                            produceEarth:this.formValidate.produceEarth,
                            produceSeed:this.formValidate.produceSeed,
                            produceFertilizer:this.formValidate.produceFertilizer,
                            producePesticides:this.formValidate.producePesticides,
                            produceSow:this.formValidate.produceSow,
                            produceCultivation:this.formValidate.produceCultivation,
                            produceSpray:this.formValidate.produceSpray,
                            produceHarvest:this.formValidate.produceHarvest,
                            producePrepare:this.formValidate.producePrepare,
                            producePerson:this.formValidate.producePerson,
                            produceInsurance:this.formValidate.produceInsurance,
                            produceInterest:this.formValidate.produceInterest,
                            produceCost:this.formValidate.produceCost,
                            produceExpect:this.formValidate.produceExpect,
                            produceEstimate:this.formValidate.produceEstimate,
                            producePlantSubsidy:this.formValidate.producePlantSubsidy,
                            producePolicySubsidy:this.formValidate.producePolicySubsidy,
                            produceProfit:this.formValidate.produceProfit,
                            produceOther:this.formValidate.produceOther,
                            produceRemarks:this.formValidate.produceRemarks
                        });
                    })
                    .catch(error => {
                        
                        this.$Message.error(error);
                    });
                
            },
            getProduce(){
                let params = new URLSearchParams();
                params.append("produfactors_dept_id", sessionStorage.getItem("dept_id"));
                axios
                    .post(global.API_PATH+"produfactors/produfactors_msg_sel", params)
                    .then(response => {
                        for(let i=0;i<response.data.length;i++){
                            this.index=i+1;
                            this.data1.push({
                                produceIndex:i+1,
                                produceCategory:response.data[i].w_produfactors_cate,
                                produceEarth:response.data[i].w_produfactors_soil_cate,
                                produceSeed:response.data[i].w_produfactors_seed_price,
                                produceFertilizer:response.data[i].w_produfactors_chem_price,
                                producePesticides:response.data[i].w_produfactors_pesticide_price,
                                produceSow:response.data[i].w_produfactors_sowing_price,
                                produceCultivation:response.data[i].w_produfactors_rotary_price,
                                produceSpray:response.data[i].w_produfactors_spraying_price,
                                produceHarvest:response.data[i].w_produfactors_harvest_price,
                                producePrepare:response.data[i].w_produfactors_autusoil_price,
                                producePerson:response.data[i].w_produfactors_manmade_price,
                                produceInsurance:response.data[i].w_produfactors_insurance_price,
                                produceInterest:response.data[i].w_produfactors_accrual_price,
                                produceCost:response.data[i].w_produfactors_plantcost_sum,
                                produceExpect:response.data[i].w_produfactors_yield_num,
                                produceEstimate:response.data[i].w_produfactors_dew,
                                producePlantSubsidy:response.data[i].w_produfactors_plant_allowance,
                                producePolicySubsidy:response.data[i].w_produfactors_grov_allowance,
                                produceProfit:response.data[i].w_produfactors_pearning,
                                produceOther:response.data[i].w_produfactors_other_price,
                                produceRemarks:response.data[i].w_produfactors_remark
                            });
                        }
                    })
                    .catch(error => {
                        this.$Message.error('错误'+error);
                    });
            }
        },
        created(){
            this.getProduce();
        }
    }
</script>


<style>

</style>


