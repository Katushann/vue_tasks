<script>
export default{
  data(){
    return{
      name: '',
      filter_switch: false,
      task: {
        name: '',
        date: '2020-12-10',
        done: false,
      },
      list: [],
      filtered: [],

    }
  },
  methods:{
    addTask(){
      if(this.task.name !== '' && this.task.date !== ''){
        this.list.push([this.task.name, this.task.date, this.task.done]);
        this.task.name = '';
        this.task.date = '2020-12-10';
      }
      //console.log(document.getElementById("task_input"));
    },
    delTask(){
      if(this.list !== null){
        for (var i in this.list){
          if (this.list[i][0] === this.task.name){
            this.list.splice(i, 1);
          }
        }
        this.task.name = '';
      }
    },
    doneTask(index){
      if(this.list !== null){
        this.list[index][2] = true;
      }
    },
    /*filterTasks( filtered, filter_num){
      this.filter_switch = true;
      filtered = [];
      switch (filter_num){
        case 0:
          for (var item in this.list){
            console.log(item[0]);
            if(!item[3]){
              filtered.push(item);
            }
          }
          console.log(filtered);
          break;
        case 1:
          for (let item in this.list){
            if(item[3]){
              filtered.push(item);
            }
          }
          break;
        case 2:
          this.filter_switch = false;
          break;
        default: break;
      }
    },*/
    sortTasks(list, ifName){
      if(ifName) {

        list.sort((a, b) => a[0] > b[0] ? 1 : -1);
      }
      else {
          list.sort((a, b) => a[1] > b[1] ? 1 : -1);
      }
    },
  }
}
</script>

<template>
<div class="main_box">
  <h1>Список задач {{ name==''?'______':name }}</h1>
  <div style="justify-content: normal">
    <input class="inputs" type="text" v-model="name" placeholder="введите имя" >
    <input class="inputs" type="date" v-model="task.date" placeholder="введите дату" >
    <input class="inputs" type="text" v-model="task.name" placeholder="введите новую задачу" id="task_input">
  </div>

  <button class="buttons"  v-if="name=='' || this.task.name =='' || this.task.date ==''" disabled>Введите имя</button>
  <button class="buttons"  v-else v-on:click="addTask()">Добавить в список</button>
  <button class="buttons"  v-on:click="delTask()">Удалить из списка</button>

  <h3>Задачи к исполнению:</h3>
  <table style="background: lightblue; border-radius: 20px; padding: 20px">
    <tr>
      <th> Номер </th>
      <th> <button class="buttons" v-on:click="sortTasks(this.list, true)">Задача</button> </th>
      <th> <button  class="buttons"  v-on:click="sortTasks(this.list, false)">Дата</button> </th>
      <th> Выполнено </th>
    </tr>

    <tr v-for="(it, index) in list" :key="index">
      <td class="things">{{ (index + 1) }}</td>
      <td class="things">{{ it[0] }}</td>
      <td class="things">{{ it[1] }}</td>
      <td>
        <button class="buttons"  v-if="!it[2]" v-on:click="doneTask(index)">Выполнено</button>
        <span v-else>✔</span>
      </td>
    </tr>


    <tr v-for="(it, index) in filtered" :key="index">
      <td>{{ (index + 1) }}</td>
      <td>{{ it[0] }}</td>
      <td>{{ it[1] }}</td>
      <td>
        <button class="buttons"  v-if="!it[2]" v-on:click="doneTask(index)">Выполнено</button>
        <span v-else>✔</span>
      </td>
    </tr>
  </table>
</div>

</template>
<style scoped>

</style>
