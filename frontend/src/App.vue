<template>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <div class="main">
    <div class="main-body">
      <div class="formation-nav">
        <span class="main-head">FC TEAM FORAGE</span>
        <div class="create-team-cont">
          <div class="create-btn">
            <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#e8eaed">
              <path
                d="M411-480q-28 0-46-21t-13-49l12-72q8-43 40.5-70.5T480-720q44 0 76.5 27.5T597-622l12 72q5 28-13 49t-46 21H411Zm-287 39q-23 1-39.5-9T63-481q-2-9-1-18t5-17q0 1-1-4-2-2-10-24-2-12 3-23t13-19l2-2q2-19 15.5-32t33.5-13q3 0 19 4l3-1q5-5 13-7.5t17-2.5q11 0 19.5 3.5T208-626q1 0 1.5.5t1.5.5q14 1 24.5 8.5T251-596q2 7 1.5 13.5T250-570q0 1 1 4 7 7 11 15.5t4 17.5q0 4-6 21-1 2 0 4l2 16q0 21-17.5 36T202-441h-78Zm676 1q-33 0-56.5-23.5T720-520q0-12 3.5-22.5T733-563l-28-25q-10-8-3.5-20t18.5-12h80q33 0 56.5 23.5T880-540v20q0 33-23.5 56.5T800-440ZM0-240v-63q0-44 44.5-70.5T160-400q13 0 25 .5t23 2.5q-14 20-21 43t-7 49v65H0Zm240 0v-65q0-65 66.5-105T480-450q108 0 174 40t66 105v65H240Zm560-160q72 0 116 26.5t44 70.5v63H780v-65q0-26-6.5-49T754-397q11-2 22.5-2.5t23.5-.5Z" />
            </svg>
            <span>SELECT TEAM</span>
            <div class="down-btn">
              <svg class="openselection" xmlns="http://www.w3.org/2000/svg" height="20px" viewBox="0 -960 960 960"
                width="20px" fill="#e8eaed">
                <path d="M480-344 240-584l56-56 184 184 184-184 56 56-240 240Z" />
              </svg>
            </div>
          </div>
          <div class="selection">
            <div class="available-players">
              <input type="search" class="search" v-model="searchValue" placeholder="Search" @input="searchPlayer(searchValue)" />
              <div class="filter-class">
                <div class="filter-text">
                  <p>Filter</p>
                </div>
                <div v-for="position in positionFilter">
                  <div class="position" @click="getByPosition(position)">
                    {{ position }}
                  </div>
                </div>
              </div>
              <div class="result-body">
                <div class="player-qu" @click="selectPlayer(player, 0)" v-for="player in playerquery">
                  <!-- To add selectPlayer method for toggle between upper box and lower box -->
                  {{ player }}
                </div>
              </div>
              <div class="mid-section">
                <div class="avail-text">
                  <p>Selected Players</p>
                  <div class="playercount">{{ playercount }}</div>
                </div>
                <div class="submit" @click="getFormations()">
                  <i class="fas fa-check"></i>
                </div>
              </div>
              <div class="available-body">
                <div class="selected-player" @click="selectPlayer(player, 1)" v-for="player in selectedplayers">
                  {{ player }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!--
      <div class="formation-div">

        <div
          v-if="this.formationquery != null && this.formationquery.length > 0"
          class="formation-title"
        >
          Select Formation
        </div>
        <div v-else class="formation-title">
          At Least 6 Players must be selected
        </div>

        <div class="formation-list">
          <div v-for="formation in formationquery">
            <div class="available-formation" style="color: black">
              <input
                type="radio"
                :value="formation"
                name="Formations"
                v-model="selectedFormation"
              />
              <label for="{{ formation }}">{{ formation }}</label>
            </div>
          </div>
          <div
            class="generate"
            v-if="this.formationquery != null && this.formationquery.length > 0"
            @click="formTeams()"
          >
            Form Teams
          </div>
        </div>
      </div>
      -->
      <div class="output-frame">
         <div class="field-border">
              <div class="team-formation">
              <div class="formation-team-title">{{ this.displayFormation }}</div>
              <div class="team-col">
                <div v-for="pos in team1" class="team-row">
                  <div v-for="j in Object.keys(pos)" class="player">
                    <div style="text-align: center">{{ j }}</div>
                    <div class="posi-text">{{ pos[j] }}</div>
                  </div>
                </div>
              </div>
            </div>
            <div class="team-formation">
              <div class="formation-team-title">{{ this.displayFormation }}</div>
              <div class="team-col">
                <div v-for="pos in team2" class="team-row">
                  <div v-for="j in Object.keys(pos)" class="player">
                    <div style="text-align: center">{{ j }}</div>
                    <div class="posi-text">{{ pos[j] }}</div>
                  </div>
                </div>
              </div>
            </div>
         </div>
        <div class="addplayer-btn">
          <svg xmlns="http://www.w3.org/2000/svg" height="40px" viewBox="0 -960 960 960" width="40px" fill="#dad7cd">
            <path
              d="M480-80q-83 0-156-31.5T197-197q-54-54-85.5-127T80-480q0-83 31.5-156T197-763q54-54 127-85.5T480-880q83 0 156 31.5T763-763q54 54 85.5 127T880-480q0 83-31.5 156T763-197q-54 54-127 85.5T480-80Zm200-500 54-18 16-54q-32-48-77-82.5T574-786l-54 38v56l160 112Zm-400 0 160-112v-56l-54-38q-54 17-99 51.5T210-652l16 54 54 18Zm-42 308 46-4 30-54-58-174-56-20-40 30q0 65 18 118.5T238-272Zm242 112q26 0 51-4t49-12l28-60-26-44H378l-26 44 28 60q24 8 49 12t51 4Zm-90-200h180l56-160-146-102-144 102 54 160Zm332 88q42-50 60-103.5T800-494l-40-28-56 18-58 174 30 54 46 4Z" />
          </svg>
        </div>
      </div>
    </div>
    <!--
    <div class="side-body">
      <div class="available-players" v-if="isphone == false">
        <input
          type="search"
          class="search"
          v-model="searchValue"
          placeholder="Search"
          @input="searchPlayer(searchValue)"
        />
        <div class="filter-class">
          <div class="filter-text"><p>Filter</p></div>
          <div v-for="position in positionFilter">
            <div class="position" @click="getByPosition(position)">
              {{ position }}
            </div>
          </div>
        </div>
        <div class="result-body">
          <div
            class="player-qu"
            @click="selectPlayer(player, 0)"
            v-for="player in playerquery"
          >
            To add selectPlayer method for toggle between upper box and lower box
            {{ player }}
          </div>
        </div>
        <div class="mid-section">
          <div class="avail-text">
            <p>Selected Players</p>
            <div class="playercount">{{ playercount }}</div>
          </div>
          <div class="submit" @click="getFormations()">
            <i class="fas fa-check"></i>
          </div>
        </div>
        <div class="available-body">
          <div
            class="selected-player"
            @click="selectPlayer(player, 1)"
            v-for="player in selectedplayers"
          >
            {{ player }}
          </div>
        </div>
      </div>


      <div class="button-div" v-if="isphone == false">
        <router-link to="/newplayer" class="link-newplayer">
          <div
            class="addPlayer"
            @mouseover="showAddPlayerText(true)"
            @mouseout="showAddPlayerText(false)"
          >
            <i class="fas fa-plus"></i>
            <div class="hoverText" :class="{ show: isAddPlayerHovered }">
              <p>Add New Player</p>
            </div>
          </div>
        </router-link>
      </div>
      <div class="button-div" v-if="isphone == true">
        <div class="selectPlayers">
          <div style="font-size: 8px; text-align: center">
            Select<br />Players
          </div>
          <router-link to="/selectPlayers" class="link-selectplayers">
            <i class="fas fa-user" style="text-align: center"></i>
          </router-link>
        </div>
        <div class="addPlayer">
          <div style="font-size: 8px; text-align: center">Add<br />Player</div>
          <router-link to="/newplayer" class="link-newplayer">
            <i class="fas fa-plus"></i>
          </router-link>
        </div>
        <div class="viewDatabase">
          <div style="font-size: 8px; text-align: center">
            View<br />Databse
          </div>
          <router-link to="/database" class="link-database">
            <i class="fas fa-database"></i>
          </router-link>
        </div>
      </div>
    </div>
        -->
  </div>

  <router-view></router-view>
</template>

<script>
import axios from "axios";
import NGROK_TUNNEL from "../public/constants.js";
export default {
  data() {
    return {
      isAddPlayerHovered: false,
      positionFilter: ["A", "M", "D", "G"],
      playerquery: [],
      selectedplayers: [],
      selectedFormation: "",
      displayFormation: "",
      playercount: 0,
      searchValue: "",
      isphone: false,
      formationquery: null,
      positions: {
        Goalkeeper: ["GK"],
        Defender: ["RB", "LB", "CB"],
        Midfielder: ["CDM", "RM", "LM", "CM", "CAM"],
        Attacker: ["RW", "LW", "CF", "ST"],
      },
      showTeam: true,
      team1: [],
      team2: [],
    };
  },
  mounted() {
    window.addEventListener("resize", this.checkOrientation);
    this.checkOrientation();
    this.openSelection();
  },
  methods: {
    searchPlayer() {
      const parameter = {
        str: this.searchValue,
        present_players: this.selectedplayers,
      };
      this.playerquery = [];
      axios
        .get(NGROK_TUNNEL + "/api/players/search_player", {
          headers: {
            "ngrok-skip-browser-warning": "true",
          },
          params: parameter,
        })
        .then((response) => {
          console.log(response.data);
          response.data.forEach((element) => {
            this.playerquery.push(element.name);
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
    checkOrientation() {
      if (
        window.matchMedia("(max-width: 700px) and (orientation: portrait)")
          .matches
      ) {
        this.isphone = true;
      } else {
        this.isphone = false;
      }
    },
    getFormations() {
      this.selectedFormation = "";
      this.displayFormation = "";
      this.team1 = [];
      this.team2 = [];
      axios
        .get(NGROK_TUNNEL + "/api/formations", {
          headers: {
            "ngrok-skip-browser-warning": "true",
          },
          params: { no_p: this.playercount, selected_p: this.selectedplayers },
        })
        .then((res) => {
          this.formationquery = res.data;
          console.log(this.formationquery);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getByPosition(category) {
      console.log(this.selectedFormation);
      let cat;
      this.playerquery = [];
      if (category == "A") cat = "Attacker";
      else if (category == "M") cat = "MidFielder";
      else if (category == "D") cat = "Defender";
      else if (category == "G") cat = "GoalKeeper";
      axios
        .get(NGROK_TUNNEL + "/api/players/player_by_category", {
          headers: {
            "ngrok-skip-browser-warning": "true",
          },
          params: { category: cat, present_players: this.selectedplayers },
        })
        .then((r) => {
          console.log("Hi");
          r.data.forEach((element) => {
            this.playerquery.push(element.name);
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
    selectPlayer(p, flag) {
      if (flag == 0) {
        this.selectedplayers.push(p);
        this.playerquery = this.playerquery.filter((item) => item !== p);
      } else if (flag == 1) {
        this.selectedplayers = this.selectedplayers.filter(
          (item) => item !== p
        );
        this.playerquery.push(p);
      }
      this.checkselectedplength();
    },
    checkselectedplength() {
      if (this.selectedplayers == null || this.selectedplayers == undefined)
        this.playercount = 0;
      else this.playercount = this.selectedplayers.length;
    },
    formTeams() {
      this.displayFormation = this.selectedFormation;
      this.team1 = [];
      this.team2 = [];
      const defender = {
        2: ["CB1", "CB2"],
        3: ["LB", "CB", "RB"],
        4: ["LB", "CB1", "CB2", "RB"],
      };
      const midfielder = {
        1: ["CM"],
        2: ["CM1", "CM2"],
        3: ["LM", "CM", "RM"],
        4: ["CAM", "CM1", "CM2", "CDM"],
      };
      const attacker = {
        1: ["ST"],
        2: ["ST1", "ST2"],
        3: ["LW", "ST", "RW"],
        4: ["LW", "ST1", "ST2", "RW"],
      };
      this.showTeam = true;
      const catl = this.selectedFormation.split("-");
      console.log("selected Players: ", this.selectedplayers);
      console.log("catl: ", catl);
      let Team1, Team2;
      axios
        .post(NGROK_TUNNEL + "/api/teams", {
          players: this.selectedplayers,
          formation: catl,
        })
        .then((response) => {
          Team1 = response.data.Team[0];
          Team2 = response.data.Team[1];
          console.log(Team1["GK"], Team2);
          for (let i = 0; i < 4; i++) {
            if (i == 3) {
              this.team1.push({ GK: Team1["GK"] });
              this.team2.push({ GK: Team2["GK"] });
            } else if (i == 2) {
              let d1 = {};
              let d2 = {};
              for (let j of defender[catl[1]]) {
                d1[j] = Team1[j];
                d2[j] = Team2[j];
              }
              this.team1.push(d1);
              this.team2.push(d2);
            } else if (i == 1) {
              let m1 = {};
              let m2 = {};
              for (let j of midfielder[catl[2]]) {
                m1[j] = Team1[j];
                m2[j] = Team2[j];
              }
              this.team1.push(m1);
              this.team2.push(m2);
            } else if (i == 0) {
              let a1 = {};
              let a2 = {};
              for (let j of attacker[catl[3]]) {
                a1[j] = Team1[j];
                a2[j] = Team2[j];
              }
              this.team1.push(a1);
              this.team2.push(a2);
            }
          }
          console.log("TEAM 1:", this.team1);
          console.log("TEAM 2:", this.team2);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    openSelection(){
      document.addEventListener("DOMContentLoaded",()=>{
        let btn=document.getElementsByClassName("create-btn")[0];
        btn.addEventListener("click",()=>{
          document.getElementsByClassName("create-team-cont")[0].classList.toggle("create-team-cont-open");
          document.getElementsByClassName("selection")[0].classList.toggle("selection-open");
        })
      })
    }
  },
};
</script>

<style>
@import url("./static/App.css");

.player-qu,
.selected-player {
  background-color: rgb(232, 232, 232);
  transition: 0.1s;
  cursor: pointer;
  width: 98%;
  border-radius: 6px;
  margin-left: auto;
  margin-right: auto;
  user-select: none;
}

.player-qu:hover,
.selected-player:hover {
  background-color: rgb(201, 201, 201);
  transform: scale(1.02);
  cursor: pointer;
}
</style>
