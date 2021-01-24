<template>
      <div class="filter">
          <div class="filter-name">{{filter}}</div>
          <div class="delete-filter"
          v-on:click="deleteFilter(filter)"><strong>X</strong></div>
      </div>
</template>

<script>

export default {
  name: 'App',
  components: {

  },
  props : {
      filter : String,
  },
  data () {
    return {
      
    }
},
methods : {
    deleteFilter : function (filter) {
        this.$emit("deleteFilter" , filter);
    }
}
}
</script>

<style scoped>
/* Desktop design */
.filter{
    display: inline-flex;
    line-height: 30px;
    margin-right: 15px;
}

.filter-name{
    background-color: hsl(180, 52%, 96%);
    color: hsl(180, 29%, 50%);
    padding-inline-end: 10px;
}

.delete-filter{
    background-color: hsl(180, 29%, 50%);
    border-radius: 0px 5px 5px 0px;
    color:white;
    cursor: pointer;
    height: 30px;
    text-align: center;
    width: 30px;
}

.delete-filter:hover{
    background-color: hsl(180, 14%, 20%);
}

/* Responsive mobile design (375px) */
@media only screen and (max-width: 375px){
    .filter{
        margin: 0px 15px 15px 0px;
    }
    .filter-name{
        font-size: 10px;
        line-height: 10px;
        padding: 10px;
    }
  
}
</style>
