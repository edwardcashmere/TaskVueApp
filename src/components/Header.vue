<template>
    <header>
         <h1>{{title}}</h1>
         <Button v-show="homePage" @btn-click="$emit('btn-click')" :text="show ? 'Close':'Add Text'" :color="show? 'red':'green' "/>
    </header>
</template>


<script>
import Button from './Button'
export default {
    name: 'Header',
    props:{
    title: String,
    show: Boolean
},
components:{
    Button
},
 computed:{
        homePage(){
            if(this.$route.path ==="/"){
                return true;
            }else{
                return false;
            }

        }

    },
}


</script>

<style scoped>

header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
    align-items: center;
}

</style>