<template>
  <div class="main col-9 col-s-11">
        <div class="main-selected-filters-container col-12 col-s-12"
        v-if="selectedFiltersArr.length > 0">
        <Filters
        v-for="filter in selectedFiltersArr"
        v-bind:key ="filter"
        v-bind:filter="filter"
        v-on:deleteFilter ="deleteFilter($event)"/>
        <div class="clear-btn"
        v-on:click ="clearFilters()">Clear</div>
        </div>
        <div class="main-job-ads-container" :style= "[selectedFiltersArr.length > 0 ? {'margin-top' :'0px'} : {'margin-top' :'55px'}]">
              <Jobs 
              v-for="jobAdd in filteredArr"
              v-bind:key="jobAdd.id"
              v-bind:jobAdd ="jobAdd" 
              v-on:addFilter="addNewFilter($event)" />
        </div>
      </div>
</template>

<script>
import Jobs from './job-adds.vue'
import Filters from './selected-filters.vue'
export default {
  components : {
    Jobs,
    Filters,
  },
props : {
  jobAdds : Object,
},
data () {
    return {
      jobAdd : this.jobAdds,
      selectedFiltersArr :  [],
    }
},
computed :{
    // filteredArr is a function that displays all job adds that match users selected filters  
    // if none of the filters is selected function returns all of the ads 
    filteredArr : function () {
      if (this.selectedFiltersArr.length == 0) {
        return this.jobAdds;
      }
    // if user has selected an filter then the function filters the list and returns all adds that match all filters   
    return this.jobAdds.filter (filter =>{
      // counter is used to count how many filters does the add match 
      var counter = 0;
      // for loop that goes through all selected filters 
      for (let i = 0 ; i < this.selectedFiltersArr.length ; i++){
        // if blok that checks if the selected filter matches adds role or level properties
        if (this.selectedFiltersArr[i] == filter.role || 
            this.selectedFiltersArr[i] == filter.level) {
            counter++;
        }
          else {
            // these two for loops were used because languages and tools properties are arrays 
            for (var j = 0 ; j < filter.languages.length; j++){
              if(this.selectedFiltersArr[i] == filter.languages[j]){
                counter++;
              }
            }
            for (var z = 0 ; z < filter.tools.length; z++){
              if(this.selectedFiltersArr[i] == filter.tools[z]){
                counter++;
              }
            }
        }
      }
      // if block that checks if the counter is equal to the number of selected filters and if true returns that add.
      if (counter == this.selectedFiltersArr.length) {
        return true;
      }
      
    })}
},
methods : {
    //function called at a click on a filter that checks if the filter is already selected
    //and if not adds that filter to the array.
    addNewFilter : function (item) {
        if (this.selectedFiltersArr.indexOf(item) === -1) {
          this.selectedFiltersArr.push(item);
        }
    },
    //function called at a click that removes selected filter 
    deleteFilter : function (filter) {
      for (let i = 0 ; i < this.selectedFiltersArr.length ; i++){
        if (this.selectedFiltersArr[i] == filter){
          this.selectedFiltersArr.splice(i,1);
        }
      }
    },
    // function that clears all selected filters 
    clearFilters : function () {
      this.selectedFiltersArr = [];
    }
    
}
}
</script>

<style scoped>
/* Desktop design */
.main{
  height: 80%;
  margin: auto;
}
/* Selected filters container  */
.main-selected-filters-container{
  background-color: white;
  padding: 20px 40px;
  position: relative;
  top: -35px;
}

.clear-btn {
  color: hsl(180, 8%, 52%);
  float: right;
  line-height: 30px;
}
.clear-btn:hover{
  color: hsl(180, 29%, 50%);
  cursor: pointer;
  text-decoration: underline;
}

/* Responsive mobile design (375px) */
@media only screen and (max-width: 375px){
    .main-selected-filters-container{
      padding: 20px 20px;
      }
    .clear-btn{
      font-size: 10px;
    }
}
</style>