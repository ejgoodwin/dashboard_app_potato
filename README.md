# dashboard_app_potato

## Run
`npm install`

`npm run dev`

## Mockup
![Designs](src/assets/readme-image.jpg)

## Plan
A Vue.js 3 project has been set up as a playground to practise Vue.js, user interaction, structure, and styling. The structure takes inspiration from the above mockups, incorporating a collapsable sidebar, header, and main section to be filled with cards of information. The primary focus is on the cards, however, if there is a desire to progress further there is room to  do this by adding tests, introducing other pages (suggestions exist in the sidebar), implementing the search functionality in the header, implementing a login,  or adding more ideas to the design and app.

The cards are laid out using css grid (2 x 2), giving each person a quarter of the available space to play with. The cards could include data from APIs, for example,  a film search,  fitness data, recipes, artwork; it could include user interaction to allow you to practise JS and DOM manipulation; it could even be a collection of your favourite dog photos; all ideas are welcome.

To add to the app, go into `src > components > widgets` to find your card component. The card components are numbered and assigned as following:

1. `One.vue` -> Alexa
1. `Two.vue` -> Purvi
1. `Three.vue` -> Erica

Make a branch and start creating!

**API keys**: if you need to use an API key, store the key in a `.env` file and add it to the gitignore file to ensure it is not pushed to GitHub.

**Submitting work**: make a pull request and add a reviewer. When the reviewer is happy they will merge the changes into the `main` branch.

### General Tasks
[ ] `In progress: Alexa` Create a CSS class for `.card`. This class will set the style of the cards to give uniformity and could include a border, border radius, and padding. This will be used by all card components, so should be set in `index.css`.

[ ] `In progress: Erica` Mobile menu. The sidebar collapses and expands on desktop but will require extra work on mobile and tablet. On smaller screens, the sidebar should be hidden from view by default and be made visible by clicking the hamburger button. A mockup can be provided if required. Please note: there is already a pull request for the expand/collapse desktop functionality [pull request #3](https://github.com/ejgoodwin/dashboard_app_potato/pull/3), so it would be advised to wait until this has been merged and build upon it.

### Useful Links
* Vue 3 docs: https://v3.vuejs.org/
* Set up Vue project with Vite: https://learnvue.co/2020/12/setting-up-your-first-vue3-project-vue-3-0-release/
