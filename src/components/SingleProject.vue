<template>
  
  <div class="project" :class="{complete: project.complete}">
    <div class="actions" >
        <h3 @click="showDetails = !showDetails">{{project.wens}}</h3>
        <div class="icons">
            <router-link :to="{ name: 'AddProject' }"><span class="material-icons"><span title="Heb je een idee hoe we deze wens kunnen vervullen?">lightbulb_outline</span></span></router-link>
            <!-- <span class="material-icons">edit</span>
            <span @click="deleteProject" class="material-icons">delete</span>
            <span @click="toggleComplete" class="material-icons tick">done</span> -->
        </div>
    </div>
    <div class="details" v-if="showDetails">
        <span v-if="wenser">
          <img src="../../data/img/user_wm.png" alt="">
            {{ project.wenser }}
        </span>
        <span v-if="datum">
          <img src="../../data/img/date_wm.png" alt="">
            {{ project.datum_str }}
        </span>
        <span v-if="location">
          <img src="../../data/img/location_wm.png" alt="">
            {{ project.locatie }}
        </span>
        <span v-if="skills">
          <img src="../../data/img/skills_wm.png" alt="">
            {{ project.skills }}
        </span>
        <span v-if="contactDetails">
          <img src="../../data/img/contact_wm.png" alt="">
            🗸
        </span>
        
        <!-- <div class="wenser">
          <img src="../../data/img/user_wm.png" alt="">
          {{ project.wenser }}
        </div>
        <div class="datum">
          <img src="../../data/img/date_wm.png" alt="">
          {{ project.datum }}
        </div>
        <div class="locatie">
          <img src="../../data/img/location_wm.png" alt="">
          {{ project.locatie }}
        </div>
        <div class="skills" v-if="skills">
          <img src="../../data/img/skills_wm.png" alt="">
          {{ project.skills }}
        </div> -->


    </div>
  </div>
</template>

<script>
export default {
    name: "SingleProject",
    props: ['project'],
    data() {
        return {
            showDetails: false,
            wenser: this.project.wenser,
            datum: this.project.datum_str,
            location: this.project.locatie,
            contactDetails: this.project.contactdetails,
            skills: this.project.skills,

            uri: 'http://localhost:3000/projects/' + this.project.id
        }
    }, 
    methods: {
        deleteProject() {
            fetch(this.uri, { method: 'DELETE'})
                .then(() => this.$emit('delete', this.project.id))
                .catch(err => console.log(err))
        },
        toggleComplete() {
          fetch(this.uri, { 
            method: 'PATCH',
            headers: { 'Content-Type': 'application/json'} ,
            body: JSON.stringify({ complete: !this.project.complete})
            }).then(() => {
              this.$emit('complete', this.project.id)
            }).catch((err) => console.log(err))
        }
    }
}
</script>

<style scoped>
  .project {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
    border-left: 4px solid #cf3963;
  }
  h3 {
    cursor: pointer;
    font-size: 24px;
  }
  .actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .icons {
    display: inline-block;
    max-height: 30px;
    min-width: 50px;
  }
  .material-icons {
    font-size: 24px;
    margin-left: 0px;
    color: #bbb;
    cursor: pointer;
  }
  .material-icons:hover {
    color: #777;
  }
  /* completed projects */
  .project.complete {
    border-left: 4px solid #40b06a
  }
  .project.complete .tick {
    color: #00ce89 
  }
  .details {
    font-size: 20px;
    
  }
  .details span{
    padding: 10px 10px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
  }
  .wenser {
    border-left:4px solid #49b0e5;
    padding: 10px 10px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
    box-sizing: content-box;
    
  }
  .datum {
    border-left:4px solid #f08100;
    padding: 10px 10px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
  }
  .locatie {
    border-left:4px solid #ffd90f;
    padding: 10px 10px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
  }
  .skills {
    border-left:4px solid #cf3963;
    padding: 10px 10px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
  }
  .details img {
    height: 20px;
  }
  
  
</style>