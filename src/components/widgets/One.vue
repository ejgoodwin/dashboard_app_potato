<template>
  <div class="widget-one">
    <h2 class="widget-one__header">NASA</h2>
    <div v-bind="info" class="widget-one__title">{{info.title}}</div>
    <div v-bind="info" >
      <img v-bind:src="info.url" class="widget-one__image">
      <p v-bind="info">{{info.explanation}}</p>
    </div>
    <div v-bind="info" class="widget-one__date">{{info.date}}</div>
  </div>
</template>

<script>

console.log(import.meta.env)
export default {
  name: 'WidgetOne',
  data () {
    return {
      info: {}
    }
  },
  mounted: function() {
    fetch(`https://api.nasa.gov/planetary/apod?api_key=${import.meta.env.VITE_NASA_API_KEY}`)
      .then(response => response.json())
      .then(data => this.info = data)
      .catch(error => console.log(error))
  },
}
</script>

<style type="text/css">
  .widget-one {
    border: solid 1px black;
	}
	
	.widget-one__header {
		text-align: center;
	}

  .widget-one__title {
    text-align: center;
  }

  .widget-one__image {
    max-width: 400px;
  }

  .widget-one__date {
    text-align: right;
    font-style: italic;
  }
</style>

