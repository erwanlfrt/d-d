<template lang="html">
    <div v-show='isActive'>
        <div>
         <p>Onglet de recherche</p>
         <item v-for='el in arr' v-if='(titles.length ? titles.includes(el[0]) : true) && (name !== "" ? el[1].toLowerCase().includes(name) : true) && (branch !== "select a branch" ? el[3].includes(branch) : true) && (school !== "select a school" ? el[2].includes(school) : true)  && (classGame !== "select a class" ? (level === "select a level" ? el[4].join(",").includes(classGame) : el[4].join(",").includes(classGame+","+level.toString())): true)'
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
                titles : [],
                name : String,
                branch : String,
                school : String,
                classGame : String,
                level : String
            }
        },
        created(){
            this.arr = JSON.parse(localStorage.getItem("values"));
            this.titles = JSON.parse(localStorage.getItem("books"));
        },
        updated(){
            //Get new standards to search for, they are stored into the local storage
            this.titles = localStorage.getItem("books");
            this.name = localStorage.getItem('name');
            this.branch = localStorage.getItem('branch');
            this.school = localStorage.getItem('school');
            this.classGame = localStorage.getItem('classGame');
            this.level = localStorage.getItem('level');
        }
    }
</script>