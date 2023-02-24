<template>
  <div id="navbar">
   <a href="#">Home</a>
   <a href="#">About</a>
   <a href="#">Contact</a>
   <a href="#">Add Employee</a>
</div>
<div id="pagdiv">
      <div v-for="item in paginatedItems" :key="item.id">{{ item.name }}</div>
    </div>
   
      <div class="pagination">
        <button id="prev" :class="{ disabled: currentPage === 1 }">
          <a  @click.prevent="currentPage -= 1">Previous</a>
        </button>
        <button  v-for="pageNumber in totalPages" :key="pageNumber" :class="{ active: pageNumber === currentPage }">
          <a  @click.prevent="currentPage = pageNumber">{{ pageNumber }}</a>
        </button>
        <button id="prev"  :class="{ disabled: currentPage === totalPages }">
          <a  @click.prevent="currentPage += 1">Next</a>
        </button>
      </div>












   <div id="maindiv">
    <table>
      <tr>
        <th>AVATAR</th>
        <th>ID</th>
        <th>NAME</th>
        <th>AGE</th>
        <th>DESIGNATION</th>
        <th>EDIT</th>
        <th>DELETE</th>
      </tr>
      <tr v-for="item in items" :key="item.id">
        <td class="td"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRd4ZB6B13vCsUxBek3yDavqdwELM4X6xqZErpHjNDEXQ&s" alt=""/></td>
        <td>{{ item.employeeid }}</td>
        <td>{{ item.firstname }}</td>
        <td>{{ item.age }}</td>
        <td>{{ item.designation }}</td>
        <td><button @click="updateItem(item.id)">Edit</button></td>
        <td><button @click="deleteItem(item.id)" >Delete</button></td>
     </tr>
    </table>
   </div>

   <div id="update">
    <h3>Edit Employee Details</h3>
    <input placeholder="Name" type="text">
    <input placeholder="Age" type="text">
    <input placeholder="Designation" type="text">
    <input placeholder="Employee Id" type="text">
    <button id="upbu">Update</button>
   </div>
  </template>
  
  <script>

  export default {
    data(){
      return {
        items:[],
        pageSize: 3,
        currentPage: 1
      }
      
    },
    methods:{
      updateItem(item){
            fetch(`https://techflitter.onrender.com/employees/${item.id}`,{
              method:"PATCH",
              headers:{
                "Content-Type":"application/json"
              },
              body:JSON.stringify(item)
            })
            .then(res=>{
               res.data
            })
            .catch(err=>{
              console.log(err);
            })
      },
        deleteItem(index){
          this.items.splice(index,1)
        }
    },
    
    
    mounted(){
      fetch("https://techflitter.onrender.com/employees")
      .then(res=>res.json())
      .then(data=>{
      this.items= data.map(item=>{
          // console.log(data);
          return {
            employeeid:item.employeeid,
            Imageurl:item.Imageurl,
            firstname:item.firstname,
            age:item.age,
            designation:item.designation
          }
         
        })
        

      })
      .catch(err=>console.log(err))
    },
    computed:{
        totalPages(){
          return Math.ceil(this.items.length/this.pageSize);
        },
        paginatedItems(){
          const startIndex=(this.currentPage-1)*this.pageSize;
          const endIndex=startIndex+this.pageSize;
          return this.items.slice(startIndex,endIndex)
        }
    },
    name: 'HelloWorld2',
  
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  body{
    margin:0;
   
  }
  #pagdiv{
 
    display: block;
    margin:auto;
    margin-top: 30px;
    
  }
  #update{
    margin-top: 30px;
    display: block;
  }
  #prev{
    border:px solid grey;
    border-radius: 3px;
    background-color:rgb(83, 142, 231) ;
    color: white;
    height: 30px;
  }
  img{
    width: 70%;
    border-radius: 50%;
  }
  button{
    outline: none;
    border: none;
    background-color: white;
    font-size: 15px;
    cursor: pointer;
  }
  button:hover{
    color:rgb(83, 142, 231)
  }
  #navbar{
      width: 100%;
      display: flex;
      /* position: static; */
      box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
      top:0;
      height: 50px;
      justify-content: space-around;
      align-items: center;
      background-color: rgb(83, 142, 231);
  }
  #navbar>a{
    text-decoration: none;
    color:white;
    font-weight: bold;
    font-size: 18px;
  }
  #navbar>a:hover{
    color:black
  }
  #maindiv{
    width: 50%;
    margin: auto;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 10px 36px 0px, rgba(0, 0, 0, 0.06) 0px 0px 0px 1px;
    margin-top: 5%;
  }
  table {
  border-collapse: separate;
  border-spacing: 0 15px;
  margin: auto;
}

th {
  background-color: black;
  color: white;
}

th,
td {
  width: 150px;
  text-align: center;
  border: 1px solid black;
  padding: 5px;
}
#upbu{
  border:1px solid grey
}
  </style>
  