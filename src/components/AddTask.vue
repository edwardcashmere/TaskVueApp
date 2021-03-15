<template>
<form @submit="onSubmit" class="add-form">
    <div class="form-control">
        <label >Add Task</label>
        <input type="text" v-model="text" name="text" placeholder="Add Task">
    </div>
    <div class="form-control">
        <label >Date & time</label>
        <input type="text" name="date" v-model="date" placeholder="Date & Time">
    </div>
    <div class="form-control form-control-check">
        <label >Set Reminder</label>
        <input type="checkbox" name="reminder" v-model="reminder">
    </div>
    <input class="btn btn-block"  value="Save Task" type="submit"/>
</form>

</template>

<script>
export default {
    name: "AddTask",
    data(){
        return {
            text:'',
            date:'',
            reminder: false
        }
    },
    methods:{
        onSubmit(e){
            e.preventDefault();

            if(!this.text){
                alert("please add task")
                return
            }

            const newTask = {
                // id: Math.floor(Math.random()*100000),
                text: this.text,
                date: this.date,
                reminder: this.reminder
            }
            // console.log(newTask)
            this.$emit("add-task", newTask)
        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}

</style>