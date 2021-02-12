<template lang="html">
    <div v-show='isActive'>
        <div>
         <p>Onglet de recherche</p>
         <item v-for='el in arr' v-if='titles.includes(el[0])'
            :name='el[1]' 
            :book='el[0]'
            :school='el[2]'
            :branch='el[3]'
            :classGame='el[4]'
            :components='el[5]'
            :time='el[6]'
            :scope='el[7]'
            :target='el[8]'
            :last='el[9]'
            :save='el[10]'
            :magicResistance='el[11]'
            :description='el[12]'
            :necessary='el[13]'
         ></item>
      </div>
        <slot></slot>
    </div>
</template>

<script>
    import Item from "./Item.vue";
    export default{
        components : {
            Item
        },
        props : {
            title : {
                type : String,
                default : "Tab"
            },
        },
        data (){
            return{
                isActive : true,
                arr : [],
                titles : []
            }
        },
        created(){
            this.arr = JSON.parse(localStorage.getItem("values"));
            this.titles = JSON.parse(localStorage.getItem("books"));

        },
        updated(){
            this.titles = localStorage.getItem("books");
            console.log("callled updated")
        }
    }
</script>