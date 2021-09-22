<template>
  <div class="editorWrapper">
    <div class="info">
      <el-divider content-position="left">JSON编辑器</el-divider>
      <span style="text-align: left">JSON编辑器编辑通常用于JSON格式配置文件、例如oss配置资源场景。</span>
    </div>
    <div>
      <el-row>
        <el-col :offset="1" :span="22">
          <div class="grid-content bg-purple-dark">
            <el-card class="box-card">
              <div style="text-align: left">
                <span>JSON编辑器</span>
                <el-divider></el-divider>
              </div>
              <div class="form-container">
                <el-form ref="form" :model="selectForm" label-width="120px">
                  <el-form-item label="主题 theme" :inline="true" label-position="right">
                    <el-select v-model="selectForm.theme" placeholder="请选择活动区域">
                      <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value"></el-option>
                    </el-select>
                  </el-form-item>
                </el-form>
              </div>
              <div class="editor-container">
                <codeJson :model-value="value" :theme="selectForm.theme" @changed="handleChanged" @input="handleInput" @update:modelValue="handleUpdate"></codeJson>
              </div>
            </el-card>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from 'vue'
import codeJson from '@/components/Editor/codeJson.vue'

const jsonData = '{"code":0,"msg":null,"data":{"records":[{"id":"12211212","productSerialNumber":"2021091000010","productName":"流动资金贷款“接续贷”","productShortName":"流动资金贷款“接续贷”","productType":"1","productLogo":"/admin/sys-file/fcsp/90aa5daa0b404f40a304837205780c7d.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"吉林银行","belongInstitutionType":"1","mainGuaranteeWay":"0","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":1.00,"amountLimitUpper":1000.00,"interestRateLimitLower":6.5300,"interestRateLimitUpper":7.1300,"interestRateShow":"","loanPeriodLimitLower":"1","loanPeriodLimitUpper":"36","repaymentWay":"1","serviceArea":"220602,220605,220621,220622,220623,220681","serviceAreaCode":"","inquiryMaterials":"1,2,7,8,10,12,13,15,16,17","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"jlbank_bs","auditStatus":"1","auditTime":"2021-09-10 09:21:59","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"464","productSerialNumber":"2021091000009","productName":"小微企业信用贷款","productShortName":"小微企业信用贷款","productType":"1","productLogo":"/admin/sys-file/fcsp/7c4cd2b93c674e87a7abc747e518982b.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"吉林银行","belongInstitutionType":"1","mainGuaranteeWay":"3","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":1.00,"amountLimitUpper":1000.00,"interestRateLimitLower":6.0900,"interestRateLimitUpper":6.5100,"interestRateShow":"","loanPeriodLimitLower":"1","loanPeriodLimitUpper":"12","repaymentWay":"1","serviceArea":"220602,220605,220621,220622,220623,220681","serviceAreaCode":"","inquiryMaterials":"1,2,7,8,10,12,13,15,16,17","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"jlbank_bs","auditStatus":"1","auditTime":"2021-09-10 09:21:58","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"463","productSerialNumber":"2021091000008","productName":"小企业个人经营性贷款","productShortName":"小企业个人经营性贷款","productType":"1","productLogo":"/admin/sys-file/fcsp/5630107a27204a91ad3106289932e09d.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"吉林银行","belongInstitutionType":"1","mainGuaranteeWay":"0","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":1.00,"amountLimitUpper":1000.00,"interestRateLimitLower":6.5300,"interestRateLimitUpper":7.1300,"interestRateShow":"","loanPeriodLimitLower":"1","loanPeriodLimitUpper":"36","repaymentWay":"1","serviceArea":"220602,220605,220621,220622,220623,220681","serviceAreaCode":"","inquiryMaterials":"1,2,7,8,10,12,13,15,16,17","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"jlbank_bs","auditStatus":"1","auditTime":"2021-09-10 09:21:56","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"462","productSerialNumber":"2021091000007","productName":"流动资金贷款","productShortName":"流动资金贷款","productType":"1","productLogo":"/admin/sys-file/fcsp/c93b4c5a940f420a911e0437a7c1435c.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"农村商业银行","belongInstitutionType":"1","mainGuaranteeWay":"3","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":1.00,"amountLimitUpper":5000.00,"interestRateLimitLower":8.6500,"interestRateLimitUpper":9.0000,"interestRateShow":"","loanPeriodLimitLower":"1","loanPeriodLimitUpper":"36","repaymentWay":"1","serviceArea":"220681","serviceAreaCode":"","inquiryMaterials":"1","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"ncsybank_lj","auditStatus":"1","auditTime":"2021-09-10 09:21:54","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"461","productSerialNumber":"2021091000006","productName":"小企业“吉税贷”","productShortName":"小企业“吉税贷”","productType":"1","productLogo":"/admin/sys-file/fcsp/aa1b0a48a008434c945f864f7e56bfab.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"吉林银行","belongInstitutionType":"1","mainGuaranteeWay":"3","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":1.00,"amountLimitUpper":200.00,"interestRateLimitLower":6.0900,"interestRateLimitUpper":6.5000,"interestRateShow":"","loanPeriodLimitLower":"1","loanPeriodLimitUpper":"12","repaymentWay":"1","serviceArea":"220602,220605,220621,220622,220623,220681","serviceAreaCode":"","inquiryMaterials":"1,2,3,7,8,10,12,13,15,16,17","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"jlbank_bs","auditStatus":"1","auditTime":"2021-09-10 09:21:51","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"460","productSerialNumber":"2021091000005","productName":"循环额度贷款","productShortName":"循环额度贷款","productType":"1","productLogo":"/admin/sys-file/fcsp/eb8a46ae11bf451594bb6249cb1cd6ad.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"农村商业银行","belongInstitutionType":"1","mainGuaranteeWay":"3","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":0.00,"amountLimitUpper":5000.00,"interestRateLimitLower":8.6500,"interestRateLimitUpper":9.0000,"interestRateShow":"","loanPeriodLimitLower":"12","loanPeriodLimitUpper":"36","repaymentWay":"1","serviceArea":"220681","serviceAreaCode":"","inquiryMaterials":"1","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"ncsybank_lj","auditStatus":"1","auditTime":"2021-09-10 09:21:49","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"459","productSerialNumber":"2021091000004","productName":"“吉政阳光贷”系列金融服务","productShortName":"“吉政阳光贷”系列金融服务","productType":"1","productLogo":"/admin/sys-file/fcsp/233c90f23f734f2a973d43e2f38389d2.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"吉林银行","belongInstitutionType":"1","mainGuaranteeWay":"0","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":1.00,"amountLimitUpper":1000.00,"interestRateLimitLower":4.3500,"interestRateLimitUpper":6.5000,"interestRateShow":"","loanPeriodLimitLower":"1","loanPeriodLimitUpper":"12","repaymentWay":"1","serviceArea":"220602,220605,220621,220622,220623","serviceAreaCode":"","inquiryMaterials":"1,2,4,7,8,10,12,13,15,16,17","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"jlbank_bs","auditStatus":"1","auditTime":"2021-09-10 09:21:45","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"458","productSerialNumber":"2021091000003","productName":"人民币循环额度贷款","productShortName":"人民币循环额度贷款","productType":"1","productLogo":"/admin/sys-file/fcsp/4548d7ef104f41ea832f65032646a7dd.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"农村商业银行","belongInstitutionType":"1","mainGuaranteeWay":"3","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":1.00,"amountLimitUpper":1000.00,"interestRateLimitLower":7.0000,"interestRateLimitUpper":8.0000,"interestRateShow":"","loanPeriodLimitLower":"12","loanPeriodLimitUpper":"36","repaymentWay":"1","serviceArea":"220622","serviceAreaCode":"","inquiryMaterials":"1","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"ncsybank_jy","auditStatus":"1","auditTime":"2021-09-10 09:21:43","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"457","productSerialNumber":"2021091000002","productName":"内部监管存货抵押贷款","productShortName":"内部监管存货抵押贷款","productType":"1","productLogo":"/admin/sys-file/fcsp/c1999dba1aae408da81dd97ef2d34b72.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"农村信用合作联社","belongInstitutionType":"1","mainGuaranteeWay":"3","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":100.00,"amountLimitUpper":1000.00,"interestRateLimitLower":6.9300,"interestRateLimitUpper":6.9300,"interestRateShow":"","loanPeriodLimitLower":"6","loanPeriodLimitUpper":"12","repaymentWay":"1","serviceArea":"220621","serviceAreaCode":"","inquiryMaterials":"1,2","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"ncbank_sf","auditStatus":"1","auditTime":"2021-09-10 09:21:41","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null},{"id":"456","productSerialNumber":"2021091000001","productName":"房闪贷","productShortName":"房闪贷","productType":"1","productLogo":"/admin/sys-file/fcsp/c744a583c4c6445485c9dfdabbafe627.png","orgLogo":null,"belongInstitution":null,"belongInstitutionName":"大连银行","belongInstitutionType":"1","mainGuaranteeWay":"3","mainGuaranteeWayName":null,"secondGuaranteeWay":"0","auditMode":"3","onlineAddressType":"","onlineAddressUrl":"","amountLimitLower":1.00,"amountLimitUpper":300.00,"interestRateLimitLower":5.0000,"interestRateLimitUpper":8.0000,"interestRateShow":"","loanPeriodLimitLower":"1","loanPeriodLimitUpper":"12","repaymentWay":"1","serviceArea":"220602,220603,220604,220605,220621,220622,220623,220625,220681","serviceAreaCode":"","inquiryMaterials":"1","sort":null,"mainRecommend":"1","fixedRecommend":"","homeRecommend":"","marketTop":"","productHot":"1","enabled":"1","applyNum":0,"publishSource":"dlbank_bs","auditStatus":"1","auditTime":"2021-09-10 09:21:39","auditor":"admin","rejectReason":null,"lastVersion":null,"organizationName":null,"productId":null,"tenantId":null,"deptId":null,"outTargetUrl":null}],"total":388,"size":10,"current":1,"orders":[],"optimizeCountSql":true,"hitCount":false,"countId":null,"maxLimit":null,"searchCount":true,"pages":39}}'
export default defineComponent({
  name: 'JsonEditor',
  components: {
    codeJson
  },
  directives: {},
  setup() {
    const value = ref(JSON.parse(jsonData))
    const options = [
      {
        value: 'shadowfox',
        label: 'shadowfox'
      },
      {
        value: 'night',
        label: 'night'
      },
      {
        value: 'rubyblue',
        label: 'rubyblue'
      },
      {
        value: 'solarized',
        label: 'solarized'
      },
      {
        value: 'material-ocean',
        label: 'material-ocean'
      }
    ]
    const state = reactive({
      selectForm: {
        theme: 'material-ocean'
      }
    })
    const handleUpdate = () => {
      console.log('sss')
    }
    const handleInput = (ev: any) => {
      value.value = JSON.parse(ev)
    }
    const handleChanged = (ev: any) => {
      value.value = JSON.parse(ev)
    }
    return {
      value,
      options,
      handleUpdate,
      handleInput,
      handleChanged,
      ...toRefs(state)
    }
  }
})
</script>
<style lang="stylus" scoped>
.form-container{
  text-align :left
}
.editor-container{
     position: relative;
  height: 100%;
}
.editorWrapper{
       margin-top:20px;

    .info{
        text-align: left;
    padding-left: 20px;
    margin-bottom: 20px;
    font-size: 12px;
    }
    .section{
      display:flex;
      flex-direction:row;
      justify-content: flex-start;
      align-items :center;
    }
     .el-row {
       margin-bottom: 20px;
     }

}
</style>
