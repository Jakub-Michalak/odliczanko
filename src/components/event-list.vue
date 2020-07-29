<template>
  <div>
    <div class="jumbotron p-4">
      <form>
        <h1 class="display-4">Zegar tyka</h1>
        <p class="lead">Dodaj wydarzenie, którego nie możesz się doczekać</p>
        <hr class="my-4">
        <div class="row">
          <div class="col">
            <label for="eventName">Na co czekasz?</label>
            <input type="text" class="form-control" id="eventName" v-model="eventName">
          </div>
          <div class="col">
            <label for="eventDate">Kiedy?</label>
            <input type="date" class="form-control" id="eventDate" v-model="eventDate">
          </div>
        </div>
        <div class="row">
          <div class="col">
            <button v-on:click="addEvent(eventName,eventDate)" type="button" class="btn btn-primary mt-4">Dodaj</button>
          </div>
        </div>
      </form>
    </div>

    <div v-for="event in events" :key="event.id">
      <h1>{{ event.name }}</h1>
      <p>{{ new Date(event.date).toLocaleDateString() }}</p>
      <Countdown v-bind:date="event.date"/>
      <button v-on:click="removeEvent(event)" type="button" class="btn btn-danger">Usuń</button>
      <hr class="my-4">
    </div>

  </div>
</template>

<script>
import Countdown from "@/components/countdown";

export default {
  name: "event-list",
  data () {
    return {
      eventName: '',
      eventDate: '',
      events: [

      ]
    }
  },
  mounted() {
    if(localStorage.getItem('events')){
      try {
        this.events = JSON.parse(localStorage.getItem('events'));
      } catch(e) {
        localStorage.removeItem('events');
      }
    }
  },
  methods: {
    addEvent: function(eventName,eventDate){
      this.events.push({
        'id': this.events.length + 1,
        'name': eventName,
        'date': eventDate
      });
      this.saveEvents();
    },
    removeEvent: function(event){
      this.events.splice(this.events.indexOf(event), 1);
      this.saveEvents();
    },
    saveEvents: function(){
      const parsed = JSON.stringify(this.events);
      localStorage.setItem('events',parsed);
    }
  },
  components: {
    Countdown
  }
}
</script>

<style scoped>

</style>