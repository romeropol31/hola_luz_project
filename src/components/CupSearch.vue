<style>
    .theme--light.v-btn.v-btn--disabled {
        color: rgba(20, 19, 19, 0.726) !important;
        background-color: lightgrey !important;
        border-color: lightgrey !important;
        cursor: not-allowed;
    }


</style>

<template>
    <v-container class="mr-0 ml-0 pa-0" fluid>
        <v-card>
            <v-img src="../assets/FrontPageImage.jpg" height="450px">
                <div class="white--text mt-15 ml-7 text-h2 font-weight-medium">Now you are the light</div>
                <div class="white--text mt-2 ml-7 text-h4 font-weight-medium">Produce.Sell.Contagious</div>
                <div class="white--text mt-2 ml-7 text-h6">Because with Holaluz you produce your own energy.</div>
            </v-img>
        </v-card>
        <div class="d-flex flex-row elevation-10 justify-center mb-5 rounded-lg" style="width:500px;height: 150px;z-index:1;margin: auto;position: relative;margin-top: -69px !important;background-color: white;">
            <v-row style="margin-top: 40px;margin-left: 25px;margin-right: 25px;">
                <v-text-field v-model="cups" label="CUPS" :rules="rules" hide-details="auto"></v-text-field>
                <v-btn elevation="2" outlined rounded  class="pink mt-3 ml-2 white--text" :disabled="cups.length == 6 && /^\d+$/.test(cups) ? false : true"  @click="checkCUPS()">Check Offers</v-btn>
            </v-row>
        </div>

        <v-card v-if="!!offer" height="200px" width="500px" style="margin:auto;">
            <v-img
              src="../assets/OfferImage.jpg"
              class="white--text align-end mt-5"
              gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
            >
              <v-card-title v-text="offer"></v-card-title>
            </v-img>
          </v-card>
    </v-container>
</template>


<script>
import Clients from '../../clients.json';
import SupplyPoints from '../../supply-points.json';
    export default {
        data: () => ({
            rules: [
                value => !!value || 'Required.',
                value => (value && value.length == 6) || '6 characters required',
                value => (/^\d+$/.test(value) && value.length == 6) ||'Only numbers allowed'
            ],
            cups: '',
            offer: '',
            client: {},
            supplyPoint:{},

        }),
        methods:{
            async getClient(cups){
                this.client = Clients.find(x => x.cups === cups);
            },
            async getSupplyPoint(cups){
                this.supplyPoint = SupplyPoints.find(x => x.cups === cups);
            },
            async checkCUPS(){
                await this.getClient(this.cups);
                await this.getSupplyPoint(this.cups);


                if(this.client == undefined){
                    this.offer = 'Client does not exist'
                    return false;
                }
                
                if(this.client.building_type != 'house'){
                    this.offer = "No offer";
                    return false;
                }

                if(this.supplyPoint.neighbors.length == 0){this.offer = "No offer"; return false;}
                
                this.supplyPoint.neighbors.forEach(neighbor => {
                    let neighborFind = SupplyPoints.find(x => x.cups == neighbor);
                    if(parseInt(neighborFind.invoiced_amount) > 100){this.offer = "12% Offer"; return true;}
                    if(this.client.p1 >= neighborFind.p1 && this.client.p2 >= neighborFind.p2){this.offer = "5% offer"; return true;}
                    this.offer = "Standard Offer 0%";
                });
                
            },
        }
    }
</script>