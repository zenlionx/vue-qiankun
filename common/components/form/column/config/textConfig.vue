<template>
    <el-row class="component-config-row">
        <el-col :span="8" class="component-config-right">
            组件id:
        </el-col>
        <el-col :span="16" class="component-config-left">
            <el-input placeholder="请输入内容" v-model="store.state.currentComponent.id"></el-input>
        </el-col>
    </el-row>
    <el-row class="component-config-row">
        <el-col :span="8" class="component-config-right">
            组件name:
        </el-col>
        <el-col :span="16" class="component-config-left">
            <el-input placeholder="请输入内容" v-model="store.state.currentComponent.name"></el-input>
        </el-col>
    </el-row>
    <el-row class="component-config-row">
        <el-col :span="8" class="component-config-right">
            组件title:
        </el-col>
        <el-col :span="16" class="component-config-left">
            <el-input placeholder="请输入组件名称" v-model="store.state.currentComponent.title"></el-input>
        </el-col>
    </el-row>
    <el-row class="component-config-row">
        <el-col :span="8" class="component-config-right">
            是否必填:
        </el-col>
        <el-col :span="16" class="component-config-left">
            <el-switch v-model="store.state.currentComponent.required"></el-switch>
        </el-col>
    </el-row>
    <el-row class="component-config-row">
        <el-col :span="8" class="component-config-right">
            占位文本:
        </el-col>
        <el-col :span="16" class="component-config-left">
            <el-input placeholder="请输入占位文本" v-model="store.state.currentComponent.placeholder"></el-input>
        </el-col>
    </el-row>
    <el-divider content-position="center">正则校验</el-divider>
    <template v-for="item in store.state.currentComponent.rules">
        <el-row class="component-config-row">
            <el-col :span="8" class="component-config-right">
                表达式:
            </el-col>
            <el-col :span="16" class="component-config-left">
                <el-input placeholder="请输入表达式" v-model="item.pattern"></el-input>
            </el-col>
        </el-row>
        <el-row class="component-config-row">
            <el-col :span="8" class="component-config-right">
                错误提示:
            </el-col>
            <el-col :span="16" class="component-config-left">
                <el-input placeholder="请输入错误提示" v-model="item.message"></el-input>
            </el-col>
        </el-row>
    </template>

     <el-button type="text" @click="createRuleClick">添加规则</el-button>
</template>
<script setup>
import { computed } from 'vue'
import { useStore } from 'vuex'
const props = defineProps({
    column: {
        type: Object,
        default: () => { },
    }
})

const store = useStore()

const componentValue = computed({
  get: function () {
    return props.column
  },
  set: function (val) {
    console.log(val, 'text-config-computed')
    emit('update:column', val)
  }
})

const createRuleClick = () => {
    // console.log(componentValue, '---------')
    // componentValue.rules =[
    //     // ...componentValue.rules,
    //     {
    //         pattern:'',
    //         message: ''
    //     }
    // ]
    store.commit('addComponentRule', 
    {
        pattern:'',
        message: ''
    })
}
console.log(props.column, '文本框的text-props-column')
</script>
<style lang="scss" scoped>

.component-config-row {
  display: flex;
  padding: 5px;
}

.component-config-right{
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding-right: 15px;
}

.component-config-left{
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding-right: 15px;
}
</style>