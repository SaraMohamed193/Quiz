<template>
   <div>
       <b-container>
  <b-nav>
    <b-nav-item disabled><b>Quiz App</b></b-nav-item>
    
   
    <b-nav-item disabled>{{correctNum}}/{{totalNum}}</b-nav-item>
  </b-nav>
  </b-container>
</div>
</template>
<script>
export default {
    props:[
        'totalNum',

        'correctNum'
    
    ]
       
}
</script>

