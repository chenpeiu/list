<template>
  <div class="todolist absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
    <div class="wrap flex-col bg-amber-100 text-slate-600 p-5 rounded-md shadow-md">
      <div class="upbar pb-5 flex">
        <label for="todo" class="text-center px-2 pl-0 text-cyan-600">待辦清單</label>
        <input type="text" id="todo" class="bg-transparent border-dotted border-2 border-cyan-500  rounded-md px-1 outline-0" v-model="todoitem" @keyup.enter="additem(todoitem)">
        <button @click="additem(todoitem)" class="text-center text-cyan-500 px-2 hover:text-cyan-800 "><fa :icon='["fas" , "circle-arrow-down"]' /></button>
      </div>
      <div class="bottombar">
        <div class="ring-2 ring-pink-500/50 rounded-sm text-center text-pink-600 mb-1 shadow-inner">Todolist</div>
        <div class="h-28 overflow-y-auto p-1">
          <div class="item flex mb-1" v-for="item in showlist" :key="item.id">
            <div class="itemname w-[85%] p-1 border-b-2 border-rose-500/20 ">{{item.itemname}}</div>
            <button class="w-[15%] bg-pink-400 rounded-lg text-white hover:text-pink-800" @click="item.done=true"><fa :icon='["fas" , "circle-check"]' /></button>
          </div>
        </div>
        <div class="ring-2 ring-amber-500/50 rounded-sm text-center text-amber-600 mb-1 shadow-inner mt-2">Donelist</div>
        <div class="h-28 overflow-y-auto p-1">
          <div class="item flex mb-1" v-for="done in donelist" :key="done.id">
            <div class="itemname w-[85%] p-1 border-b-2 border-amber-500/20 pb-1">{{done.itemname}}</div>
            <button class="w-[15%] bg-amber-400 rounded-lg text-white hover:text-amber-800" @click="dellist(done.id)"><fa :icon='["fas" , "trash-can"]' /></button>
          </div>
        </div>
        <div class="text-slate-600 text-sm mt-3">有 &#32;{{notyet}}&#32;件事項要處理</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      todoitem:'',
      todolist:[],
      addorder: 1,
      notyet:0,
    }
  },
  computed:{
    donelist(){
      return this.todolist.filter(item=>item.done==true)
    },
    showlist(){
      let result= this.todolist.filter(item=>item.done==false)
      this.notyet=result.length
      return result
    },
  },
  methods:{
    additem(item){
      if(this.todoitem!=''){
        this.todolist.push(
          {
            itemname: this.todoitem,
            done: false,
            id: this.addorder,
          }
        )
      this.addorder++
      this.todoitem=""
      }
    },
    dellist(number){
      for(let i=0;i<this.todolist.length;i++){
        if (this.todolist[i].id==number){
          this.todolist.splice(i,1)
        }
      }
    }
  }
}
</script>
