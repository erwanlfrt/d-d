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
        <input @change='refreshSearchedStandards' ref="test" type="text" placeholder="search by name" />
        <select @change='refreshSchool' id="selectedSchool">
            <option> select a school </option>
            <option v-for='el in schools' :value='el' :id='el'>{{el}}</option>
        </select>
        <select @change='refreshBranch' id="selectedBranch">
            <option> select a branch</option>
            <option v-for='el in branches' :value='el' :id='el'>{{el}}</option>
        </select>
        <select @change='refreshClassGame' id="selectedClassGame">
            <option> select a class</option>
            <option v-for='el in classesGame' :value='el' :id='el'>{{el}}</option>
        </select>
        <select @change='refreshLevel' id="selectedLevel">
            <option> select a level</option>
            <option v-for='el in 10' :value='el' :id='el'>{{el}}</option>
        </select>
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
                schools : [],
                branches : [],
                classesGame : []
            }
        },
        created(){
            //Get list of items saved into the local storage
            var tmp = JSON.parse(localStorage.getItem("values"));
            var titles = [];
            for(let i = 0; i<tmp.length ; i++){
                //get the list of titles
                if(!(titles.includes(tmp[i][0]))){
                    titles.push(tmp[i][0]);
                }
                //get the list of schools
                if(!(this.schools.includes(tmp[i][2]))){
                    this.schools.push(tmp[i][2]);
                }
                //get the list of branches
                tmp[i][3].forEach(element => {
                    if(!(this.branches.includes(element))){
                        this.branches.push(element);
                    }
                });
                //get the list of classes
                tmp[i][4].forEach(element => {
                    if(!(this.classesGame.includes(element[0]))){
                        this.classesGame.push(element[0]);
                    }
                });
            }
            this.arr = titles;
        },
        methods : {
                /**
                 * refresh the searched level
                 */
                refreshLevel(){
                    localStorage.setItem("level", document.getElementById("selectedLevel").value);
                },
                /**
                 * refresh the searched class game
                 */
                refreshClassGame(){
                    localStorage.setItem("classGame", document.getElementById("selectedClassGame").value);
                },
                /**
                 * refresh the searched school
                 */
                refreshSchool(){
                    localStorage.setItem("school", document.getElementById("selectedSchool").value);
                },
                /**
                 * refresh the searched branch
                 */
                refreshBranch(){
                    localStorage.setItem("branch", document.getElementById("selectedBranch").value);
                },
                /**
                 * refresh the searched name
                 */
                refreshSearchedStandards(){
                    localStorage.setItem('name', this.$refs.test.value.toLowerCase());
                },
                /**
                 * add a book to the list of selected book
                 */
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
                /**
                 * refresh the list of searched titles into the local storage
                 */
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
                /**
                 * delete a title to search.
                 */
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