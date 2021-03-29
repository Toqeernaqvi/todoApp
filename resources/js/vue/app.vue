<template>
  <div class="todoListContainer">
    <div class="heading">
      <h2 id="title">Todo List</h2>

      <addItemForm 
         v-on:reloadList= "getList()"
      />
    </div>
    <listView :items = "items"
    v-on:reloadList= "getList()"
    />
  </div>
</template>



<script>
import addItemForm from "./addItemForm";
import listView from "./listView";
export default {
  components: { listView, addItemForm },
  data : function(){
      return {
          items:[]
      }
  },
  methods:{
      getList(){
          axios.get('api/items')
          .then(response=>{
              this.items = response.data;
          })
          .catch(error =>{
              console.log(error);
          })
      }
  },
  created(){
      this.getList(); 
  }
};
</script>
<style scoped>
.todoListContainer {
  width: 350px;
  margin: auto;
}

.heading {
  background: #e6e6e6;
  padding: 10px;
}
#title {
  text-align: center;
}
</style>