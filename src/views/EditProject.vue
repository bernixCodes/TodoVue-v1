<template>
   <form @submit.prevent="handleupdate">
      <label>Title: </label>
      <input type="text"  v-model="title" required/>

      <label>Details: </label>
      <textarea required v-model="details"></textarea>

      <button>Update Project</button>
  </form>
</template>

<script>
export default {
    props:['id'],
data(){
      return{
          title: '',
          details: '',
            url:'http://localhost:3000/projects/' + this.id
      }
  },
  mounted(){
      fetch(this.url)
      .then(res => res.json())
      .then(data => {
          this.title = data.title;
          this.details = data.details
      })
  },
  methods:{
      handleupdate(){
          let edittedProject = {
              title: this.title,
              details: this.details
          }
          fetch(this.url,{
              method: 'PATCH',
               headers:{'Content-Type': 'application/json'},
             body: JSON.stringify(edittedProject)
          })
           .then(()=>{
             this.$router.push('/')
         })
         .catch(err =>console.log(err.message))
      }
  }
}
</script>

<style>

</style>