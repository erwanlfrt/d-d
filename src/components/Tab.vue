<template lang="html">
    <div v-show='isActive'>
        <div>
         <p>Hellow from tab</p>
      </div>
        <slot></slot>
    </div>
</template>

<script>
    export default{
        props: {
            title : {
                type : String,
                default : 'Tab'
            },
            index : {
                type : Number,
                default : 0
            }
            
        },
        data (){
            return{
                isActive : true
            }
        }
    }
</script>