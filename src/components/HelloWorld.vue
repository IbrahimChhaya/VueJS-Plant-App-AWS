<template>
  <v-container class="page fill-height">
    
    <div class="header">
      <h1 class="header-title">How are your plants today?</h1>
      <div class="subtitles">
        <p>Wednesday, 2 August</p>
        <p>
          <v-icon
            size="large"
            icon="mdi-weather-cloudy"
          />
          23°C
        </p>
      </div>
    </div>

    <v-card width="100%">
      <div class="text-h6">
          <v-icon 
            icon="mdi-alert-circle"
            size="small"
            color="#1f6d43"
            class="need-water-icon"
          />
          <p class="need-water-text">Need to Be Watered</p>
      </div>

      <div v-for="plant in plantsNew" :key="plant.plantId">
        <v-card class="plant-card">
          <v-avatar
            rounded="0"
            size="80">
            <v-img
              src="monstera.jpg"
            ></v-img>
          </v-avatar>
          <div class="plant-name">
            <div class="text-h6 q-pl-md">
                {{ plant.name }}
            </div>
            <div class="text-subtitle1 q-pl-md">
                <v-icon
                    name="water_drop"
                    color="blue-7"
                    class="q-pb-xs"
                />
                {{ plant.lastWatered }} days ago
            </div>
          </div>

          <!-- <v-btn
              flat
              color="primary"
              icon="las la-chevron-circle-right"
              class="absolute-right"
          /> -->
        </v-card>
        
        <v-divider></v-divider>
      </div>
    </v-card>

    <v-bottom-navigation bg-color="#1f6d43">
      <v-btn value="home">
        <v-icon color="white">mdi-home-outline</v-icon>
      </v-btn>

      <v-btn value="cancel" disabled>
        <v-icon color="white">mdi-cancel</v-icon>
      </v-btn>

      <v-btn value="camera">
        <span class="camera-icon-background"></span>
        <v-icon color="#1f6d43" size="50">mdi-camera-outline</v-icon>
      </v-btn>

      <v-btn value="plants">
        <v-icon color="white">mdi-leaf</v-icon>
      </v-btn>

      <v-btn value="settings">
        <v-icon color="white">mdi-cog-outline</v-icon>
      </v-btn>
    </v-bottom-navigation>

  </v-container>
</template>

<script lang="ts">

  import axios from 'axios';
  import { Plant } from '../models/plant-interface'

  export default {
    data: () => ({

      plantsNew: [] as Plant[],

      // plants: [
      //   {
      //       id: 1,
      //       name: "Monstera",
      //       lastWatered: 4,
      //       picture: "monstera.jpg",
      //   },
      //   {
      //       id: 2,
      //       name: "Spider Plant",
      //       lastWatered: 0,
      //       picture: "monstera.jpg",
      //   },
      //   {
      //       id: 3,
      //       name: "Golden Pothos",
      //       lastWatered: 17,
      //       picture: "monstera.jpg",
      //   },
      //   {
      //       id: 4,
      //       name: "Heartleaf",
      //       lastWatered: 6,
      //       picture: "monstera.jpg",
      //   },
      // ],
    }),

    methods: {
      async fetchPlants() {
        try {
          const plantResponse = await axios.get('https://rrwjwwqfl4.execute-api.us-west-2.amazonaws.com/prod/plants');
          
          plantResponse.data.plants.Items.map((plant : any) => {
            
            // this.getImage(plant.plantId)

            // var temp = {
            //   plantId: plant.plantId,
            //   name: plant.name,
            //   lastWatered: plant.lastWatered,
            //   image: 
            // }
            this.plantsNew.push(plant)
          })
          
          
        } catch (error) {
          console.error('Error fetching plants:', error);
        }
      },

      async getImage(filename: string) {
        const apiUrl = 'https://svjvs2eltj.execute-api.us-west-2.amazonaws.com/prod/download';
        const jsonData = {
          filename: filename + '.jpg',
        };

        try {
          const response = await axios.post(apiUrl, jsonData);
          console.log('Response:', response.data);
        } catch (error) {
          console.error('Error:', error);
        }
      },

      async uploadImage() {
        const apiUrl = 'https://4l2ckhec63.execute-api.us-west-2.amazonaws.com/prod/upload';
        const jsonData = {
          image:  + 'iVBORw0KGgoAAAANSUhEUgAAAQAAAAEACAIAAADTED8xAAADMElEQVR4nOzVwQnAIBQFQYXff81RUkQCOyDj1YOPnbXWPmeTRef+/3O/OyBjzh3CD95BfqICMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMK0CMO0TAAD//2Anhf4QtqobAAAAAElFTkSuQmCC',
          image_name: 'test.jpg'
        };

        try {
          const response = await axios.post(apiUrl, jsonData);
          console.log('Response:', response.data);
        } catch (error) {
          console.error('Error:', error);
        }
      }

    },

    mounted() {
      this.fetchPlants();
      // this.getImage('1001');
      this.uploadImage();
    },
  }

</script>

<style scroped lang="scss">

  .page {
    background-color: #f8f8f8;
  }

  .header {
    top: 0;
    left: 0;
    right: 0;
    position: fixed;
    height: 25%;
    display: flex;
    flex-direction: column;
    background-image: url("monsteraBackground.png");
    background-size: cover;
    filter: brightness(125%);
    padding: 15px;

    .header-title {
      color: white;
      font-size: 2.125rem;
      font-weight: 400;
      line-height: 2.5rem;
      letter-spacing: 0.00735em;
    }

    .subtitles {
      color: white;
      display: flex;
      justify-content: space-between;
    }
  }

  .need-water-icon {
    padding-bottom: 5px;
  }

  .need-water-text {
    display: inline;
    padding-left: 5px;
  }

  .plant-card {
    display: flex !important;;
  }

  .camera-icon-background {
    font-size: 50px;    
    position: fixed;
    // z-index: 999;
    background-color: white;
    bottom: 3px;
    padding: 25px;
    border-radius: 50%;
    border-style: solid;
  }

</style>