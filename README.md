# Quiz
  You have to answer 10 questions about comics.  

  This project is made with vuejs

  Made partly in https://bootstrap-vue.org/  
  Calling https://opentdb.com/ API  
  Using https://lodash.com/ library

  Thanks to Gwen Faraday ! I lived code with her for this project

  https://www.youtube.com/watch?v=4deVCNJq3qc&list=RDCMUC8butISFwT-Wl7EV0hUK0BQ&start_radio=1

  I get rid of Bootstrap Vue
  I added some functionnalities and I modified the visual of the page according to my taste.

  Some more functionnalities mmight be added to this project in order to maximise the UI

  - Add a component to display the final score on the 10th question
  - Choose quiz by theme in adding a parent component which will call the API depending of the choosen theme
  - let the user choose the number of questions he wants to answer
  - Possibility of connection ---> COUPLER AVEC Node.JS en BACK !!!!

  ### Logical

  How many variables do I need ?
  - An answer has been selected --> selectedIndex
  - Method which put the index selected into it --> selectAnswer()
  - Submit & Next Button disabled until the answer has not been submitted
  - Only Submit button enabled when an answer has been selected
  - Only Next Button enabled when an answer has been submitted
  - Method which verify if the selected Index is the right answer on clicking on Submit --> submitAnswer()
  - Method which colorize the answers depends on if the answer has been selected or submitted (right or wrong)
    in order to let the user know about his response. 


## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
