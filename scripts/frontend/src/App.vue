<template>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <div class="main">
    <div class="main-body">
      <div class="formation-div">
        <div v-if="this.formationquery!=null && this.formationquery.length>0" class="formation-title">Select Formation</div>
        <div v-else class="formation-title">At Least 7 Players must be selected</div>
        <div class="formation-list">
          <div v-for="formation in formationquery">
            <div class="available-formation" style="color: black;">
              <input type="radio" :value="formation" name="Formations" v-model="selectedFormation">
              <label for="{{ formation }}">{{ formation }}</label>
            </div>
          </div>
          <div class="generate" v-if="this.formationquery!=null && this.formationquery.length>0" @click="formTeams()">Form Teams</div>
        </div>
      </div>
      <div class="output-frame">
        <div class="team-formation">
        </div>
        <div class="team-formation">
        </div>
      </div>
    </div>
    <SideFrame></SideFrame>
  </div>
    
  <router-view></router-view>
</template>

<script>
  import axios from 'axios'
  import SideFrame from "./components/SideFrame.vue";
  export default {
    components: {
      SideFrame,
    },
    data() {
      return {
        formationquery: null,
        positions: {
        'Goalkeeper': ['GK'],
        'Defender': ['RB', 'LB', 'CB'],
        'Midfielder': ['CDM', 'RM', 'LM', 'CM', 'CAM'],
        'Attacker': ['RW', 'LW', 'CF', 'ST']
        },
        showTeam:true,
        team1:{},
        team2:{}
      };
    },
    mounted() {
    window.addEventListener('resize', this.checkOrientation);
    this.checkOrientation();
  },
    methods: {
      formTeams(){
        this.showTeam = true
        const catl = this.selectedFormation.split('-')
        for(i=0;i<catl.length;i++){
          team1[i]=0
        } 
      }
    },
  };
</script>

<style>
  @import url("./static/App.css");
</style>

