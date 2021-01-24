<template> 
<!--Html template. Including Header and Main component and passing data to main component. -->
  <Header />  
  <Main :jobAdds="jobAdds" /> 
</template>

<script>
// Importing components from the components folder.
import Header from './components/header.vue'
import Main from './components/main.vue'


export default {
  name: 'App',
  components: {
    // Registering components so they can be used.
    Header,
    Main,
    
  },
  data () {
    return {
      jobAdds : []
    }
},
created () {
    // GET request from data.json using fetch with error handling
  fetch("/data.json")
    .then(async response => {
      const data = await response.json();

      // check for error response
      if (!response.ok) {
        // get error message from body or default to response statusText
        const error = (data && data.message) || response.statusText;
        return Promise.reject(error);
      }

      this.jobAdds = data;
    })
    .catch(error => {
      this.errorMessage = error;
      console.error("There was an error!", error);
    });
}
}
</script>

<style>
@font-face {
  font-family: "Spartan";
  src: local("Spartan"),
   url(./fonts/Spartan-VariableFont_wght.ttf) format("truetype");
}
*{
  box-sizing: border-box;
  font-family: "Spartan";
  font-size: 15px;
  font-weight: 500 700;
  margin: 0;
  padding: 0;
}
body {
  background-color: hsl(180, 52%, 96%);

}
/*  Responsive design for mobile (375px) and desktop (1440px)     */
@media only screen and (min-width: 375px) {
  /* For mobile: */
  .col-s-1 {width: 8.33%;}
  .col-s-2 {width: 16.66%;}
  .col-s-3 {width: 25%;}
  .col-s-4 {width: 33.33%;}
  .col-s-5 {width: 41.66%;}
  .col-s-6 {width: 50%;}
  .col-s-7 {width: 58.33%;}
  .col-s-8 {width: 66.66%;}
  .col-s-9 {width: 75%;}
  .col-s-10 {width: 83.33%;}
  .col-s-11 {width: 91.66%;}
  .col-s-12 {width: 100%;}
}

@media only screen and (min-width: 1440px) {
  /* For desktop: */
  .col-1 {width: 8.33%;}
  .col-2 {width: 16.66%;}
  .col-3 {width: 25%;}
  .col-4 {width: 33.33%;}
  .col-5 {width: 41.66%;}
  .col-6 {width: 50%;}
  .col-7 {width: 58.33%;}
  .col-8 {width: 66.66%;}
  .col-9 {width: 75%;}
  .col-10 {width: 83.33%;}
  .col-11 {width: 91.66%;}
  .col-12 {width: 100%;}
}
</style>
