<template>
  <div class="main">
   <v-card>
        <v-card-title>
          <span class="headline">Add Item</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Name*"
                  v-model="formValues.name"
                  required
                ></v-text-field>
              </v-col>
                <v-col
                cols="12"
                sm="6"
              >
                <v-select
                  :items="['micro', 'contract', 'brewpub', 'regional', 'planning', 'proprietor']"
                  label="Brewery Type*"
                  v-model="formValues.brewery_type"
                  required
                ></v-select>
              </v-col>
               <v-col
                cols="12"
                sm="6"
              >
                <v-select
                  :items="countries"
                  v-model="formValues.country"
                  label="Country"
                ></v-select>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="State"
                  v-model="formValues.state"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="City"
                  v-model="formValues.city"
                ></v-text-field>
              </v-col>
               <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Phone"
                  v-model="formValues.phone"
                ></v-text-field>
              </v-col>
                <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Website_url"
                  v-model="formValues.website_url"
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="$emit('input', false)"
          >
            Close
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="submit"
          >
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
  </div>
</template>
<script>
import Countries from '@/assets/scripts/countries.js';

  export default {
      props:{
          value: Boolean,
      },
    data () {
      return {
        dialog: false,
        formValues: {
          name: null,
          brewery_type: null,
          country: null,
          state: null,
          city: null,
          phone: null,
          website_url: null,
        },
      }
    },
   computed:{
       countries(){
           return Countries.map(data => data.name);
       }
   },
   methods:{
       submit(){
         if(this.formValues.name && this.formValues.brewery_type) {
           console.log(this.formValues);
           this.$emit('submit', this.formValues);
           this.$emit('input', false);
           this.formValues={};
         }else {
          alert('Name or Brewery Type required');
        }
       }
   }
  }
</script>
<style scoped>

</style>