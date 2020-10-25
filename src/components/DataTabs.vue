<template>
<div class>
 <h2>NASA Asteroid Information</h2>
<p>Click on the Below Menu Items to see relevant data</p>

<div class="tab">
  <button class="tablinks" v-on:click="openTab($event,'asteroid_display')" id="defaultOpen">Top 10 Asteroids Display</button>
  <button class="tablinks" v-on:click="openTab($event, 'search_by_date')">Search Asteoids by Date</button>
  <button class="tablinks" v-on:click="openTab($event, 'search_by_id')">Search Asteroids by ID</button>
</div>
        <div id="asteroid_display" class="tabcontent">  
        <Asteroid />
        </div>
        <div id="search_by_date" class="tabcontent"> 
        <AsteroidSearchByDate />     
        </div>
        <div id="search_by_id" class="tabcontent"> 
        <h3>Tokyo</h3>        
        </div>
</div>
</template>
<script>
import Asteroid from './Asteroid'
import AsteroidSearchByDate from './AsteroidSearchByDate'
export default {
  name: "DataTabs" ,
  components: {
    Asteroid,
    AsteroidSearchByDate
  },
  methods : {
      openTab (evt, tabName) {
        
           var i, tabcontent, tablinks;
            tabcontent = document.getElementsByClassName("tabcontent");
              for (i = 0; i < tabcontent.length; i++) {
                 tabcontent[i].style.display = "none";
               }
           tablinks = document.getElementsByClassName("tablinks");
                for (i = 0; i < tablinks.length; i++) {
                    tablinks[i].className = tablinks[i].className.replace(" active", "");
                }
            document.getElementById(tabName).style.display = "block";
            evt.currentTarget.className += " active";
      }
  }
};
</script>
<style scoped>
  body {font-family: Arial;}

/* Style the tab */
.tab {
  overflow: hidden;
  border: 1px solid #ccc;
 background-color: #f1f1f1;
  margin-left: auto;
  margin-right: auto;
  width:50%;
}

/* Style the buttons inside the tab */
.tab button {
   background-color: inherit;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  transition: 0.3s;
  font-size: 17px;
  width:30%;
 
}

/* Change background color of buttons on hover */
.tab button:hover {
  background-color: #ddd;
}

/* Create an active/current tablink class */
.tab button.active {
  background-color:darkgray;
}

/* Style the tab content */
.tabcontent {
  display: none;
  padding: 6px 12px;
  border: 1px solid #ccc;
  border-top: none;
}

/* Style the close button */
.topright {
  float: right;
  cursor: pointer;
  font-size: 28px;
}
</style>