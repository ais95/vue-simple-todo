<template>
    <main>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
        <h1>Task list</h1>
        <div class="input-group mb-3">
            <input type="text" class="form-control" placeholder="Recipient's username" aria-label="Recipient's username" aria-describedby="basic-addon2" v-model="getInputText">
            <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="submit" @click="submitList()">Add List</button>
            </div>
        </div>
        <ul class="list-group" style="max-height: 420px; overflow-y: auto">
            <li class="list-group-item d-flex justify-content-between align-items-center" v-for="(item, index) in items" :key="index">
                <span>{{item.title}}</span>           
                <!-- <button class="badge badge-success badge-pill" @click="markAsDone(e)">Mark as Done</button> -->
                <button class="badge badge-danger badge-pill" @click="removeEventListener(index)">X</button>
            </li>   
        </ul>
    </main>
</template>

<script>   
    import { mapState } from 'vuex';
    export default {
        data(){
            return {
                getInputText: '',
                items: [],
            }
        },
        methods:{
            computed: mapState({
                count: state => state.count,
                doneTodosCount () {
                    return this.$store.state.todos.filter(todo => todo.done).length
                },
                    count () {
      return this.$store.state.count
    }
                

            }),
            increment() {
                this.$store.commit('increment')
                console.log(this.$store.state.count)
            },
            submitList(){
                if(this.getInputText == ''){
                    alert('please enter text');
                }
                else{
                    this.items.push({title: this.getInputText});
                }
                this.getInputText = '';
            },
            markAsDone(e){
                let new_obj = {...this.items[e], isDone: true}
                console.log(new_obj)
            },
            removeEventListener(index){
                let text = "Press a button!\nEither Remove or Not.";
                if (confirm(text) == true) {
                    this.items.splice(index,1)
                } 
                else {
                    return;
                }
            }
        }
    }
</script>
