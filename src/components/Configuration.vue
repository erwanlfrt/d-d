<template lang="html">
    <div v-show='isActive'>
        <div>
         <select id="books">
             <option disabled>select a book</option>
             <option v-for='el in arr' :value='el' :id='el'>{{el}}</option>
        </select>
        <button @click='addBook()'>add</button>
        <button @click='deleteBook()'>delete</button>

        <select id="selectedBooks">
            <option disabled>list of selected books</option>
        </select>
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
                arr : []
            }
        },
        created(){
            var tmp = JSON.parse(localStorage.getItem("values"));
            var titles = [];
            for(let i = 0; i<tmp.length ; i++){
                if(!(titles.includes(tmp[i][0]))){
                    titles.push(tmp[i][0]);
                }
            }
            this.arr = titles;
        },
        methods : {
                addBook(){
                    var books = document.getElementById("books");
                    var value = books.value;
                    books.remove(books.selectedIndex);
                    
                    var selectedBooks = document.getElementById("selectedBooks");
                    var option = document.createElement("option");
                    option.value = value;
                    option.innerText = value;
                    option.id = value;
                    selectedBooks.appendChild(option);
                    this.refreshSelectedBooks();

                    
                },
                refreshSelectedBooks(){
                    var books = document.getElementById("selectedBooks");
                    var selectedBooks = [];
                    for(let i = 0 ; i< books.options.length ; i++){
                        if(books.options[i].disabled === false){
                            selectedBooks.push(books.options[i].value);
                        }
                    }      
                    localStorage.setItem("books", selectedBooks);
                },
                deleteBook(){
                    var selectedBooks = document.getElementById("selectedBooks");
                    var value = selectedBooks.value;
                    selectedBooks.remove(selectedBooks.selectedIndex);
                    
                    var books = document.getElementById("books");
                    var option = document.createElement("option");
                    option.value = value;
                    option.innerText = value;
                    option.id = value;
                    books.appendChild(option);
                    this.refreshSelectedBooks();
                }
            }
    }
</script>