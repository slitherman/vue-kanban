<template>
  
    

  <div class="container mt-5 justify-content">
    <form @submit.prevent="addCard">
      <div class="row">
        <div class="col form-inline">
          <div class="form-group">
            <label for="taskTitle">Task Title</label>
            <input
              type="text"
              class="form-control"
              id="taskTitle"
              v-model="newTask"
              required
              placeholder="Enter Task Title"
            />
          </div>
          <div class="form-group ml-3">
            <label for="taskDescription">Task Description</label>
            <input
              type="text"
              class="form-control"
              id="taskDescription"
              v-model="taskDescription"
              required
              placeholder="Enter Task Description"
            />
          </div>
          <button type="submit" class="btn btn-primary ml-3 mt-2">Add A Card</button>
        </div>
      </div>
    </form>
    </div>


   


    <div class="row mt-5">
      <div class="col-3">
        <div class="p-2 ">
          <h3>Backlog</h3>
          <draggable
            class="list-group kanban-column"
            v-model="itemArrBackLog"
            group="tasks"
         
          >
          <template v-slot:item="{element}">
            <div
              class="list-group-item"
              :key="element.id"
            >
              {{ element.name }}
              {{ element.desc }}
            </div>
          </template>
          </draggable>
        </div>
      </div>

      <div class="col-3">
        <div class="p-2 ">
          <h3>Doing</h3>
  
          <draggable
            class="list-group kanban-column"
            v-model="itemArrInProgress"
            group="tasks"
          >
          <template v-slot:item="{element}">
  
            <div
              class="list-group-item"
             
              :key="element.id"
            >
            {{ element.name?.length ? element.name : ''}}
            {{ element.desc?.length ? element.desc : '' }}
            </div>
          </template>
          </draggable>
        </div>
      </div>

      <div class="col-3">
        <div class="p-2 ">
          <h3>Testing</h3>
 
          <draggable
            class="list-group kanban-column"
            v-model="itemArrTested"
            group="tasks"
          >
          <template v-slot:item="{element}">
   
            <div
              class="list-group-item"
             
              :key="element.id"
            >
            {{ element.name?.length ? element.name : ''}}
            {{ element.desc?.length ? element.desc : '' }}
            </div>
          </template>
          </draggable>
        </div>
      </div>

      <div class="col-3">
        <div class="p-2 ">
          <h3>Done</h3>
      
          <draggable
            class="list-group kanban-column"
            v-model="itemArrDone"
            group="tasks"
          >
          <template v-slot:item="{element}">
    
            <div
              class="list-group-item"
             
              :key="element"
            >
            {{ element.name?.length ? element.name : ''}}
            {{ element.desc?.length ? element.desc : '' }}
            </div>
          </template>
          </draggable>
        </div>
      </div>
    </div>

</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "kanban-board",
  components: {
    draggable,
  },
  data() {
    return {
      drag: false,
      newTask: "", 
      taskDescription: "",
  
      itemArrBackLog: [
        { id:1, name: "Title: Kali Linux setup", 
        desc: "Description: Install OracleVm And Kali Linux"},
        { id:2, name: "Title: Dos Attacks", 
        desc: "Description: Research Dos attacks" },
        { id:3, name: "Title: Tools", 
        desc: "Description: Download Dos tools then dos yourself" },
      ],
      itemArrInProgress: [], 
      itemArrTested: [], 
      itemArrDone: [],
    };
  },
  methods: {
    addCard() {
      if (this.newTask.length !== 0 && this.taskDescription.length !== 0) {
        let title = "Title: ";
        let desc = "Description: "
        this.itemArrBackLog.push({
          name: title+= this.newTask, 
          desc: desc+= this.taskDescription,
          id:this.itemArrBackLog.length +1 
         
        });
        console.log(this.itemArrBackLog)
        this.newTask = ""; 
        this.taskDescription = "";
      }
    },
  },
};
</script>

<style>
.kanban-column {
  min-height: 300px;
  background-color: grey;
}

</style>