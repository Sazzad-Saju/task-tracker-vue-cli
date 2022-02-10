<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-control">
            <label>Task</label>
            <input type="text"  v-model="text" name="text" placeholder="Add Task">
        </div>
        <!-- {{text}} show data for binding with v-model -->
        <div class="form-control">
            <label>Day & Time</label>
            <input type="text" v-model="day" name="day" placeholder="Add day & Time">
        </div>
        <div class="form-control form-control-check">
            <label>Set Reminder</label>
            <input type="checkbox" v-model="reminder" name="reminder">
        </div>
        <input type="submit" value="Save Task" class="btn btn-block">
    </form>
</template>

<script>
    export default{
        name: 'AddTask',
        data(){
            return{
                text: '',
                day: '',
                reminder: false
            }
        },
        methods:{
            onSubmit(e){
                e.preventDefault()
                if(!this.text){
                    alert('Please add a task')
                    return
                }
                const newTask = {
                    id: Math.floor(Math.random() * 100000),
                    text: this.text,
                    day: this.day,
                    reminder: this.reminder
                }

                //store in LS:
                let Total_Tasks;
                let existsTasks = false;
                if(localStorage.getItem('Total_Tasks') === null){
                    Total_Tasks = [];
                }else{
                    Total_Tasks = JSON.parse(localStorage.getItem('Total_Tasks'));
                }
                Total_Tasks.forEach(item =>{
                    if (item.text == newTask.text){
                        alert(`Task (${item.text} Already Exists!`);
                        existsTasks = true;
                    }
                })
                if(existsTasks != true){
                    Total_Tasks.push(newTask);
                    localStorage.setItem('Total_Tasks',JSON.stringify(Total_Tasks))
                }


                //**********************
                // console.log(newTask)
                this.$emit('add-task',newTask)
                
                this.text= ''
                this.day = ''
                this.reminder = false
            },
        }
    }
</script>

<style scoped>
.add-from{
    margin-bottom: 40px;
}
.form-control{
    margin: 20px 0;
}
.form-control label {
    display: block;
}
.form-control input{
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 17px;
}
.form-control-check{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.form-control-check label{
    flex: 1;
}
.form-control-check input{
    flex: 2;
    height: 20px;
}
</style>