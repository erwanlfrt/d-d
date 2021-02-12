<template lang="html">
<div @click='hideOrShow()' style="border:solid">
    <h2>{{name}}</h2>
    <div class="more" v-show='isActive' style = "background : #d9dbd3 ; border:solid" >
        <p><strong>Book : </strong>{{book}}</p>
        <p><strong>School : </strong>{{school}}</p>
        <div>
            <p><strong>Branch : </strong></p>
            <p v-for='b in branch'>{{b}}</p>
        </div>
        <div>
            <p><strong>Class : </strong></p>
            <p v-for='c in classGame'>{{c}}</p>
        </div>
        <div>
            <p><strong>Components : </strong></p>
            <p v-for='c in components'>{{c}}</p>
        </div>
        <p><strong>Time : </strong>{{time}}</p>
        <p><strong>Scope : </strong>{{scope}}</p>
        <p><strong>Target : </strong>{{target}}</p>
        <p><strong>Last : </strong>{{last}}</p>
        <p><strong>Save : </strong>{{save}}</p>
        <p><strong>Magic resistance : </strong>{{magicResistance}}</p>
        <p><strong>Description : </strong>{{description}}</p>
        <p><strong>Necessary : </strong>{{necessary}}</p>
    </div>
    <slot></slot>
</div>
</template>

<script>
export default {
    props:{
        name : {
            type : String,
            default : 'name'
        },
        book : 
        {
            type : String,
            default : ""
        },
        school: {
            type : String,
            default : ""
        },
        branch: {
            type : Array
        },
        classGame: {
            type : Array
        },
        components: {
            type : Array
        },
        time: {
            type : String,
            default : ""
        },
        scope: {
            type : String,
            default : ""
        },
        target: {
            type : String,
            default : ""
        },
        last: {
            type : String,
            default : ""
        },
        save: {
            type : String,
            default : ""
        },
        magicResistance: {
            type : String,
            default : ""
        },
        description: {
            type : String,
            default : ""
        },
        necessary: {
            type : String,
            default : ""
        }
    },
    data () {
        return{
            isActive : false
        }
    },
    methods : {
        hideOrShow(){
            this.isActive = !this.isActive;
        }
    }
}
</script>