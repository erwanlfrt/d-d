<template lang="html">
  <div>
    <div style="display : flex; justify-content : center; flex-direction : row ">
        <button  v-for='(tab,index) in tabs'  :key='tab.title' @click='selectTab(index)'>
          {{ tab.title }}
        </button>
    </div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  data () {
    return {
      selectedIndex: 0,
      tabs: []         
    }
  },
  created () {
    this.tabs = this.$children
  },
  mounted(){
      this.selectTab(0); //default, select the tab n°0
  },
  methods : {
      selectTab(i){
          this.selectedIndex = i;
          this.tabs.forEach((tab,index) =>{
              tab.isActive = (index === i);
          })
      }
  }
}
</script>