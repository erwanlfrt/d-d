<template lang="html">
    <div v-show='isActive'>
        <div>
         <p>Onglet de stat</p>
      </div>
        <slot></slot>
    </div>
</template>

<script>
    export default{
        props : {
            title : {
                type : String,
                default : "Tab"
            }
        },
        data (){
            return{
                isActive : true
            }
        }
    }
</script>