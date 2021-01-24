<template>
    <div class="job-add" :style= "[jobAdd.featured ? {'border-left' :'5px solid hsl(180, 29%, 50%)'} : {}]">
        <img class="job-add-logo" v-bind:src= "jobAdd.logo " alt="logo" >
        <div class="job-add-info">
            <div class="job-add-info-header">
               <div class="header"> {{ jobAdd.company}}</div>
               <div class="new" v-if="jobAdd.new">NEW!</div>
               <div class="featured" v-if="jobAdd.featured">FEATURED</div>
            </div>
            <div class = "job-add-info-position"><strong>{{jobAdd.position}}</strong></div>
            <ul class="job-add-info-tags">
                <li>{{jobAdd.postedAt}}</li>
                <li>{{jobAdd.contract}}</li>
                <li>{{jobAdd.location}}</li>
            </ul>    
        </div>
        <div class="job-add-filters">
            <ul>
                <li class="job-add-filters-tags" 
                v-bind:key="item" 
                v-for="item in filtersArr "
                v-on:click="addFilter(item)" >
                {{item}}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
props :{
    jobAdd : Object,
    
},
emits : ["addFilter"],
data (){
    return {
        filtersArr : [this.jobAdd.role, this.jobAdd.level],
    }
},
mounted (){
    // 2 for loops used to fill filtersArr with filters from languages and tools properties
    for (var i = 0 ; i < this.jobAdd.languages.length; i++){
        this.filtersArr.push(this.jobAdd.languages[i]);
    }
    for (var j = 0 ; j < this.jobAdd.tools.length; j++){
        this.filtersArr.push(this.jobAdd.tools[j]);
    }
},
methods : {
    //function that emits an event to parent component and passes filter.Event is used to select a new filter.  
    addFilter : function (item) {
        this.$emit("addFilter", item);
    }
}
}

</script>

<style scoped> 
 /* Desktop design */ 

.job-add {
    background-color: white;
    border-radius: 2%;
    box-shadow: 0px 5px 10px rgb(216,236,237);
    display: flex;
    height: 100%;
    margin: 0px 0px 20px 0px;
    padding: 35px 40px;
}

.job-add-logo {
    border-radius: 50%;
    height:85px;
    margin-right: 25px;
    width: 85px;
}

.job-add-info{
    flex-grow: 1;
}

.job-add-info-header{
    display: flex;
    flex-wrap: nowrap;
    line-height: 15px;
    margin-bottom: 10px;
}

.header {
    color: hsl(180, 29%, 50%)
}

.new {
    background-color: hsl(180, 29%, 50%);
    border-radius: 10px;
    color: white;
    font-size: 10px;
    height: 20px;
    margin: 0px 15px 0px 10px;
    padding: 5px;
    text-align: center;
    width: 50px;
}

.featured {
    background-color: hsl(180, 14%, 20%);
    border-radius: 10px;
    color: white;
    font-size: 10px;
    height: 20px;
    padding:5px;
    text-align: center;
    width: 80px;
}

.job-add-info-position{
    cursor: pointer;
    margin-bottom: 10px;
}

.job-add-info-tags{
    padding-inline-start: 0px;
}

.job-add-info-tags :first-child{
    list-style-type: none;
}

.job-add-info-tags > li{
    color: hsl(180, 8%, 52%);
    float: left;
    padding-right: 30px;
}

.job-add-filters {
    flex-grow: 1;
    padding-top:25px;
}

.job-add-filters-tags{
    background-color: hsl(180, 52%, 96%);
    border-radius: 5px;
    color:hsl(180, 29%, 50%);
    cursor: pointer;
    float:right;
    height: 30px;
    line-height: 10px;
    list-style-type: none;
    margin-left: 20px;
    padding: 10px;
}

.job-add-filters-tags:hover{
    background-color: hsl(180, 29%, 50%);
    color:white;
}
/* Responsive mobile design (375px) */
@media only screen and (max-width: 375px){
  .job-add{
      flex-direction: column;
      margin: 40px 0px 40px 0px;
      padding: 30px 25px;
  }

  .job-add-logo{
    height: 50px;
    position: relative;
    top: -60px;
    width: 50px;
  }

  .job-add-info{
      border-bottom: 1px solid hsl(180, 8%, 52%);
      margin-top: -50px;
      padding-bottom: 20px;
  }

  .new,.featured{
      font-size: 10px;
      line-height: 15px;
      padding: auto;
  }

  .header {
      font-size: 10px;
      line-height: 25px;
  }

  .job-add-info-position{
      margin-bottom: 20px;
  }

  .job-add-info-tags > li {
      font-size: 10px;
      line-height: 20px;
      padding-right: 20px;
  }

  .job-add-filters{
      padding-top: 0px;
  }

  .job-add-filters-tags{
      float:left;
      font-size: 10px;
      margin: 15px 15px 0px 0px;
  }
  
}
</style>