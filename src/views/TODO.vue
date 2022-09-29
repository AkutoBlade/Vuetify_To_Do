<template>
  <div class="home">
    <v-text-field
            outlined
            label="Add Task"
            append-icon="mdi-plus"
            class="pa-3"
            color="orange"
            hide-details
            clearable
            v-model="Task"
            @click:append="AddTask"
            @keyup.enter="AddTask"
          ></v-text-field>
    <v-list
     class="pt-0"
      flat
    >
    <div v-for="task in tasks" :key="task.id">
      <v-list-item @click="doneTask(task.id)" 
       :class="{'grey lighten-2': task.done}"
      >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="orange"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{'text-decoration-line-through': task.done}">{{task.title}}</v-list-item-title>
            </v-list-item-content>
            
            <v-list-item-action>
          <v-btn  icon>
            <v-icon v-if="task.done" @click.stop="deleteTask(task.id)" color="orange">mdi-delete</v-icon>
            <v-icon v-else color="grey lighten-1">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
    </div>
    
    </v-list>
  </div>
</template>

<script>

  export default {
    name: 'Home',
    data(){
      return {
        Task:'',
        tasks:[
        // {
        //   id: 1,
        //   title:'Drink Water',
        //   done:false
        // },
        // {
        //   id: 2,
        //   title:'Wake Up',
        //   done:false
        // },
        // {
        //   id: 3,
        //   title:'Morning Jog',
        //   done:false
        // }
        ]
      }
    },
    methods:{
      doneTask(id){
        let task = this.tasks.filter(task => task.id === id)[0];
        task.done = !task.done
      },
      deleteTask(id){
        this.tasks = this.tasks.filter(task => task.id !== id)
      },
      AddTask(){
        let item = {
          id: this.tasks.length +1,
          title: this.Task,
          done:false
        }
        this.tasks.push(item)
      }
    }
  }
</script>
