<template>
  <div class="alert alert-primary">
    <h1 v-if="finished">Odliczanie zakończone!</h1>
    <div v-if="!finished" class="row">
      <div class="col-3">
        <h1>{{displayDays}}</h1>
        <p class="mb-0">Dni</p>
      </div>
      <div class="col-3">
        <h1>{{displayHours}}</h1>
        <p class="mb-0">Godzin</p>
      </div>
      <div class="col-3">
        <h1>{{displayMinutes}}</h1>
        <p class="mb-0">Minut</p>
      </div>
      <div class="col-3">
        <h1>{{displaySeconds}}</h1>
        <p class="mb-0">Sekund</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "countdown",
  props: ['date'],
  data () {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      finished: false
    }
  },
  computed: {
    _seconds: function () {
      return 1000
    },
    _minutes: function (){
      return this._seconds * 60
   },
    _hours: function (){
      return this._minutes * 60
    },
    _days: function (){
      return this._hours * 24
    }
  },
  mounted() {
    this.showRemaining()
  },
  methods: {
    showRemaining(){
      const timer = setInterval(()=>{
        const now = new Date();
        const end = new Date(this.date);
        const distance = end.getTime() - now.getTime();

        if(distance < 0){
          clearInterval(timer);
          this.finished = true;
        }

        const days = Math.floor((distance / this._days));
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance%this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.displayDays = days;
        this.displayHours = hours;
        this.displayMinutes = minutes;
        this.displaySeconds = seconds;

      })
    }
  }
};
</script>

<style scoped>

</style>