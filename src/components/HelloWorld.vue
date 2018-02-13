<template>
  <div>
<div class="doing">
  <h3>Pending tasks</h3>
  <textarea v-model="task" @keyup.enter="add"></textarea>
  
  <ul>
    <li v-for="item in tasks" @dblclick="move_to_done(`${item}`)">{{item}}</li>
  </ul>
</div>
<div class="done">
  <h3>Completed tasks</h3>
  <ul>
    <li v-for="item in done" @dblclick="remove(`${item}`)">{{item}}</li>
  </ul>
</div>
 </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
    tasks:[],
    task: "",
    done:[]
  }
  },
  mounted()
  {
    if (localStorage.getItem('doingkey')) 
      this.tasks = JSON.parse(localStorage.getItem('doingkey'));
      if (localStorage.getItem('donekey')) 
      this.done = JSON.parse(localStorage.getItem('donekey'));
  },

  methods:{
    add(){
      this.tasks.push(this.task);
      this.task='';
      console.log(this.tasks);
      localStorage.setItem("doingkey", JSON.stringify(this.tasks));
    

    },
    move_to_done(item){
      console.log(item);
      this.done.push(item);
      var index=this.tasks.indexOf(item);
      this.tasks.splice(index,1);
      localStorage.setItem("donekey", JSON.stringify(this.done));
      localStorage.setItem("doingkey", JSON.stringify(this.tasks));
    },
    remove(item)
    {
      var index=this.done.indexOf(item);
      console.log(index);
      this.done.splice(index,1);
      localStorage.setItem("donekey", JSON.stringify(this.done));
    },
    initialise_tasks()
    {
      if(this.tasks!=null)
      this.tasks = JSON.parse(localStorage.getItem("doingkey"));
      
    },
    initialise_done()
    {
      if(this.done!=null)
      this.done= JSON.parse(localStorage.getItem("donekey"));
    }

  }
 
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  text-align: center;
  padding: 0;
  list-style-type: none;
}
button
{
  background-color: blue;
  height: 50px;
  width: 50px;
  border-radius: 5px;
  color:white;
}
li {
 
  border:1px solid gray;
  margin:20px 10px 0px 10px;
  
  
  border-radius: 5px;
 
}
a {
  color: #42b983;
}

textarea
{
  border-color: gray;
  border-radius: 5px;
  width: 30%;
}
.doing, .done
{
  
  width:300px;
  background-color: #E2E4E6;
 margin-left: 5%;
  display: inline-table;
  border-radius: 10px;
  position: relative;
  margin-top: 5%;
  
}

</style>
