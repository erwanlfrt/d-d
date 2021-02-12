<template lang="html">
    <div v-show='isActive'>
        <div>
         <p>Onglet de stat</p>
         <p><strong>Nombre de livres :</strong>{{statBooks}}</p>
         <p><strong>Nombre de sorts : </strong>{{spells}}</p>
         <div>
             <p><strong>Nombre de sorts par livre : </strong></p>
             <p v-for='books in spellsInBooks'>{{books[0]}} : {{books[1]}}</p>
         </div>
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
                isActive : true,
                arr : [],
                statBooks : 0,
                spellsInBooks : new Map(),
                spells : 0,
            }
        },
        created(){
            this.arr = JSON.parse(localStorage.getItem("values"));
            this.statBooks = this.countBooks();
            this.spellsInBooks = this.countSpellsInBooks();
            this.spells = this.countSpells();
        },
        methods : {
            countBooks(){
                var cpt = 0;
                var titles = [];
                for(let i=0 ; i<this.arr.length ; i++){
                    if(!(titles.includes(this.arr[i][0]))){
                        titles.push(this.arr[i][0]);
                        cpt++;
                    }
                }
                return cpt;
            },
            countSpells(){
                return this.arr.length;           
            },
            countSpellsInBooks(){
                var res = new Map();
                for(let i=0 ; i<this.arr.length ; i++){
                    if(res.get(this.arr[i][0]) !== undefined){
                        res.set(this.arr[i][0], res.get(this.arr[i][0])+1)
                    }
                    else{
                        res.set(this.arr[i][0], 1);
                    }
                }
                return res;
            }
        }
    }
</script>