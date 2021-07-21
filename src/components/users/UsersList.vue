<template>
  <button @click='saveChanges'>Save Changes</button>
  <ul>
    <user-item v-for="user in users" :key="user.id" :name="user.fullName" :role="user.role"></user-item>
  </ul>
</template>

<script>
import UserItem from './UserItem.vue';

export default {
  components: {
    UserItem,
  },
  data(){
    return{
      changesSaved:false,
    }
  },
  methods:{
    saveChanges(){
      this.changesSaved=true;
    }
  },
  inject: ['users'],
  beforeRouteEnter(to,from,next){
    console.log('UsersList Comp beforeRouteEnter');
    console.log(to,from);
    next();
  },
  beforeRouteLeave(to,from,next){
    console.log('UsersList Comp beforeRouteLeave');
    console.log(to,from);

    if(this.changesSaved){
      next();
    }else{
      let userWantsToLeave=confirm('Are you sure? You got unsaved changes!');
      next(userWantsToLeave);
    }
  },
  unmounted() {
    console.log('unmounted');
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 2rem auto;
  max-width: 20rem;
  padding: 0;
}
</style>