<template>
  <div class="widget-one">
      <div v-bind="info" class="widget-one__date">{{info.date}}</div>
    <div>
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
    display: flex;
    flex-direction: column;
    padding: 0 10px 20px 10px;
	}

  .widget-one__date {
    font-style: italic;
    text-align: right;
  }
	
	.widget-one__header {
    font-size: 28px;
    margin: 10px;
    text-align: center;
	}

  .widget-one__title {
    padding-bottom: 5px;
    text-align: center;
  }

  .widget-one__button-container {
    margin-bottom: 5px;
    padding: 10px;
  }

  .widget-one__button {
    background-color: #081727;
    border: 1px solid;
    border-radius: 8px;
    box-shadow: 0 7px 15px rgba(0, 0, 0, 0.2);
    color: white;
    display: block;
    margin: 0 auto;
    padding: 10px;
  }

  .widget-one__button:hover {
    background-color: #263955;
  }

  .widget-one__content-container {
    display: inline-block;
  }
  .widget-one__image {
    display: block;
    margin: 0 auto;
    max-height: 400px;
    object-fit: contain;
  }

  .widget-one__explanation {
    max-height: 75%;
    overflow: scroll;
    padding: 10px;
  }

  @media screen and (max-width: 800px) {
    .widget-one__date {
      font-size: 12px;
    }

    .widget-one__header {
      margin: 10px 0;
    }

    .widget-one__button {
      font-size: 12px;
      padding: 5px;
    }

    .widget-one__image {
      max-width: 100%;
    }

    .widget-one__explanation {
      max-height: 300px;
    }
  }
</style>
