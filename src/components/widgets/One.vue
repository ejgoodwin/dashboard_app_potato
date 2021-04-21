<template>
  <div class="widget-one">
      <div v-bind="info" class="widget-one__date">{{info.date}}</div>
    <div class="widget-one__header-date-container">
      <h2 class="widget-one__header">NASA</h2>
    </div>
    <div v-bind="info" class="widget-one__title">{{info.title}}</div>
    <div class="widget-one__button-container">
      <button v-on:click="toggleFunction" class="widget-one__button">{{buttonText}}</button>
    </div>
    <div class="widget-one__content-container">
      <div v-if="toggle === true">
        <img v-bind:src="info.url" class="widget-one__image">
      </div>
      <div v-else>
        <p v-bind="info" class="widget-one__explanation">{{info.explanation}}</p>
      </div>
    </div>
  </div>
</template>

<script>

console.log(import.meta.env)
export default {
  name: 'WidgetOne',
  data () {
    return {
      info: {},
      toggle: true,
      buttonText: 'Explanation'
    }
  },
  mounted: function() {
    fetch(`https://api.nasa.gov/planetary/apod?api_key=${import.meta.env.VITE_NASA_API_KEY}`)
      .then(response => response.json())
      .then(data => this.info = data)
      .catch(error => console.log(error))
  },
  methods: {
    toggleFunction: function() {
      this.toggle = !this.toggle
      if (this.toggle) {
        this.buttonText = 'Explanation'
      } else {
        this.buttonText = 'Image'
      }
    }
  },
}
</script>

<style type="text/css">
  .widget-one {
    border: solid 1px black;
    padding: 0 10px 20px 10px;
    display: flex;
    flex-direction: column;
	}
	
	.widget-one__header {
    text-align: center;
    margin: 10px;
    font-size: 28px;
	}

  .widget-one__title {
    padding-bottom: 5px;
    text-align: center;
  }

  .widget-one__content-container {
    /* max-height: 100px; */
    /* border: 5px red solid; */
    /* margin: 15px 0; */
    display: inline-block;
  }
  .widget-one__image {
    display: block;
    max-height: 400px;
    object-fit: contain;
    margin: 0 auto;
  }

  .widget-one__explanation {
    max-height: 200px;
    overflow: scroll;
  }

  .widget-one__header-date-container {
    /* display: flex; */
    /* flex-direction: row; */
    /* justify-content: flex-end; */
  }

  .widget-one__date {
    text-align: right;
    font-style: italic;
    /* align-self: center; */
  }

  .widget-one__button-container {
    padding: 10px;
    margin-bottom: 5px;
    /* display: inline-block; */
    /* border: solid 5px red; */
    /* width: 100%; */
    /* justify-content: center; */
  }

  .widget-one__button {
    /* position: absolute; */
    display: block;
    margin: 0 auto;
    padding: 10px;
    border: 1px solid;
    background-color: #081727;
    color: white;
    border-radius: 8px;
    box-shadow: 0 7px 15px rgba(0, 0, 0, 0.2);
  }

  .widget-one__button:hover {
    background-color: #263955;
  }

  @media screen and (max-width: 800px) {
    .widget-one__header {
      margin: 10px 0;
    }

    .widget-one__date {
      font-size: 12px;
    }

    .widget-one__button {
      padding: 5px;
      font-size: 12px;
    }

    .widget-one__image {
      max-width: 100%;
    }
  }
</style>
