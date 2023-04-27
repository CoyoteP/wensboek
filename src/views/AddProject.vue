<template>
  <form @submit.prevent="handleSubmit">
    <label>Wens:</label>
    <input type="text" v-model="wish">
    <label>Naam:</label>
    <input type="text" v-model="name">
    <label>Locatie:</label>
    <input type="text" v-model="location">
    <!-- <label>Datum:</label>
    <input type="date" v-model="date" required> -->
    <label>Vaardigheden:</label>
    <textarea v-model="skills"></textarea>
    <label>ID:</label>
    {{database[-1]}}
    <button>Doe een wens!</button>
  </form>
  
</template>

<script>
var dt = new Date();

var dt = dt.getUTCDate() + "/" + (dt.getUTCMonth() + 1) + "/" + dt.getUTCFullYear();
console.log(dt)
export default {
    data() {
        return {
            wish: '',
            name: '',
            location: '',
            date: dt,
            
            skills: '',
            database: []
        }
    },
    mounted() {
      fetch('http://localhost:3000/wishes')
        .then(res => res.json())
        .then(data => this.database = data)
        .catch(err => console.log(err))
      
      console.log('hello' + this.database[0])
    },
    methods: {
        handleSubmit() {
            let project = {
                wens: this.wish,
                wenser: this.name,
                locatie: this.location,
                datum: this.date,
                skills: this.skills,
                complete: false
            }
            console.log(this.date)
            console.log(this.skills)

            fetch('http://localhost:3000/wishes', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(project)
            }).then(() => {
                this.$router.push('/')
            }).catch(err => console.log(err))
        }
    }
}
</script>

<style>
  form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
  }
</style>