<template>
  <!-- Main div -->
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background:#1a2330;">
    <!-- calculator result div -->
    <div class="w-full rounded m-1 p-4 text-end lead font-weight-bold text-white bg-vue-darkcolor">
      {{calDefaultValue || 0 }}
    </div>
    <!-- calculator input buttons -->
    <div class="row no-gutters">  
      <div class="col-3" v-for="ele in calElements" :key="ele">
        <div class="lead text-white text-center bg-vue-darkcolor m-1 py-3 rounded hover-class"
        :class="{'bg-vue-yellow': ['C','*','/','-','+','%','='].includes(ele)}"
        @click="action(ele)">
          {{ ele }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  props: {
    msg: String,
  },
  data() {
    return {
      calDefaultValue: '',
      previousResult: '',
      calElements: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      operator: null,
      
    };
  },
  methods:{
    action(ele){
      // append user value
      if(!isNaN(ele) || ele == "."){
        this.calDefaultValue += ele + "";
      }
      // clear input
      if (ele === 'C') {
        this.calDefaultValue = '';
      }
      if (ele === '%') {
        this.calDefaultValue = this.calDefaultValue / 100 + '';
      }
      // get operators
      if(['/','*','-','+'].includes(ele)){
        this.operator = ele;
        this.previousResult = this.calDefaultValue;
        this.calDefaultValue = '';
      }
      if (ele === '=') {
        this.calDefaultValue = eval(
          this.previousResult + this.operator + this.calDefaultValue
        );
        this.previousResult = '';
        this.operator = null;        
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-vue-darkcolor {
  background: #273344;
}
.hover-class:hover {
  cursor: pointer;
  background: #ff9500;
}
.bg-vue-yellow{
  background: #ff9500;
}
 
</style>
