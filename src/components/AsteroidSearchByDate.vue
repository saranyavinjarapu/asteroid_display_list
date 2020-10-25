<template>
<div> 
  <form @submit="processForm($event)">
  <label for="start_date">Pick a Start Date : </label>
  <input type="date" v-model="start_date" ><br><br>
  <label for="end_date">Pick an End Date : </label>
  <input type="date" v-model="end_date" ><br><br>
  <input type="submit" value="Submit" >
  </form> 
  
    <table id="asteroid_table_by_date">  <tr>
    <th>Asteroid Name</th>
    <th>Asteroid Id</th> 
    <th>NASA JPN URL</th>
  </tr>
  <tr v-for="asteroidDataByDate in asteroidDataByDateList" :key="asteroidDataByDate.id">
    <td>{{asteroidDataByDate.name}}</td>
    <td>{{asteroidDataByDate.id}}</td>
    <td>{{asteroidDataByDate.nasa_jpl_url}}</td>      
  </tr> 
  
</table>
</div>   
</template>

<script>

export default {
  name: "AsteroidSearchByDate",
  data() {
    return {
        start_date:'',
        end_date:'',        
       asteroidDataByDateList: []
    };
  },
  methods: {

    async processForm (form_event) {
         form_event.preventDefault();        
        const apiKey = 'ydl7nVUxNWm2Vid24ecGBL3L6R6dp8fHXbT4NfZO';              
        try {         
          const response = await fetch(
         `https://api.nasa.gov/neo/rest/v1/feed?start_date=${this.start_date}&end_date=${this.end_date}&api_key=${apiKey}`);
          const newData =  await response.json();          
          const near_earth_objects_data = newData.near_earth_objects;

           console.log('final', near_earth_objects_data);
            const  finalAsteroidDataByDate =[];
              for(var i=0;i<10;i++)
              {
                finalAsteroidDataByDate.push(near_earth_objects_data[i]);
              }
             this.asteroidDataByDateList = finalAsteroidDataByDate;
            
             
           
           } 
       catch (error) {    
          console.log('error');
         }   

    }
 
  }
};
</script>
<style scoped>

.search_form {
   margin-top: auto;
   margin-right: auto;
   margin-left: auto;
   padding-top: 10px;
   border : 1px solid black;
   width:55%;
   height:200px;
   padding-top: 30px;
  
   }
label  {
    font-size:25px
    }


table {
  width:80%;
  margin-left: auto;
  margin-right: auto;
  padding-top: 50px;
  
}

th, td {
  border: 1px solid black;
  border-collapse: collapse;
   padding: 15px;
  text-align: left;
}

#asteroid_table_by_date tr:nth-child(even) {
  background-color: #eee;
}
#asteroid_table_by_date tr:nth-child(odd) {
 background-color: #fff;
}
#asteroid_table_by_date th {
  background-color: black;
  color: white;
}

 input[type=submit] {
  padding-top: 1px;
  background-color: #1aa832;
  color: white;
  border: 1px solid #ccc;
  height:50px; 
  width:400px;
  font-size: 30px;
}
button {
 padding-top: 1px;
  background-color: #1aa832;
  color: white;
  border: 1px solid #ccc;
  height:50px; 
  width:400px;
  font-size: 30px;
 
}
</style>