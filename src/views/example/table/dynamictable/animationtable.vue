<template>
    <div class="app-container">
        <div class="filter-container">
            <el-checkbox-group v-model="checkboxVal"	>
                <el-checkbox label="apple">apple</el-checkbox>
                <el-checkbox label="banana">banana</el-checkbox>
                <el-checkbox label="orange">orange</el-checkbox>
            </el-checkbox-group>
        </div>
       <div style="width: 100%;height:100%;" :class="{kuozhan:kuozhan}">
       <div class="left">
        <el-table :data="tableData" :key='key' style="width: 100%">

            <el-table-column v-for='(fruit,index) in formThead' :key='fruit'  :label="fruit">
                <template scope="scope">
                    {{scope.row[fruit]}}
                </template>
            </el-table-column>

        </el-table>
        </div >
           <!--这个是连动的效果 -->
           <transition name="fade">
           <div class="staitic">
              <el-button @click="change()">click</el-button>
           </div>
           </transition>
           <!-- 这是连动的效果 -->
       </div>
        <!--这个是研究Vue的动画效果-->

      <div id="demo">
          <button v-on:click="show = !show">
              toggle
          </button>
          <transition name="fade">
              <p v-if="show">Hello</p>
          </transition>
      </div>

        <!--这个是研究Vue的动画效果-->

    </div>
</template>

<style>
    .staic {
        float: left;
    }
   .left {
       float:left;

       width:70%;
   }
    .kuozhan .left{
        transition: transform 2s;
        width:90%;

    }
    .kuozhan .right {
      width:0;
    }

    .fade-enter-active, .fade-leave-active {
        transition: opacity 2.5s;
    }

    .fade-enter, .fade-leave-to {
        opacity: 0;
    }
</style>


<script>

    const defaultFormThead = ['apple', 'banana']; // 默认选中项
    export default {
        methods:{
            change(){
                 console.log("kai");
                 this.kuozhan = !this.kuozhan;
              },
            toggleShow() {
               this.isShowing = !this.isShowing;
          }
        },
        data() {
        return {
            isShowing: false,
            kuozhan:false,
            show:true,
            items:['apple','banana','orange'],
            tableData: [
                {
                    name: 'fruit-1',
                    apple: 'apple-10',
                    banana: 'banana-10',
                    orange: 'orange-10'
                },
                {
                    name: 'fruit-2',
                    apple: 'apple-20',
                    banana: 'banana-20',
                    orange: 'orange-20'
                }
            ],
            key: 1, // table key
            formTheadOptions: ['apple', 'banana', 'orange'], // 可选择表头
            checkboxVal: defaultFormThead, // checkboxVal
            formThead: defaultFormThead // 默认表头
        }
    },
    watch: {
        checkboxVal(valArr,oldVal) {
            console.log(oldVal);
            console.log(valArr);
            // this.formThead = this.formTheadOptions.filter(i => valArr.indexOf(i) >= 0);
            this.formThead = this.formTheadOptions.filter(function(x,i){
                console.log(x);
                return valArr.indexOf(x) >= 0;
            });
            this.key = this.key + 1;// 为了保证table 每次都会重渲 （牺牲性能保证效果，当然也可以不用）
        }
    },

    };
</script>

