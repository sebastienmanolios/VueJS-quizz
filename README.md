# Quiz
  You have to answer 10 questions about comics.  

  This project is made with vuejs

  Made partly in https://bootstrap-vue.org/  
  Calling https://opentdb.com/ API  
  Using https://lodash.com/ library

  Thanks to Gwen Faraday ! I lived code with her for this project

  https://www.youtube.com/watch?v=4deVCNJq3qc&list=RDCMUC8butISFwT-Wl7EV0hUK0BQ&start_radio=1

  I am going to add some more functionnalities

  - Improve mobile vizualization
  - Add a component to display the final score on the 10th question
  - Choose quiz by theme in adding a parent component which will call the API depending of the choosen theme
  - let the user choose the number of questions he wants to answer
  - Possibility of connection ---> COUPLER AVEC Node.JS en BACK !!!!

  ### Logical

  How many variables do I need ?
  1- An answer has been selected --> selectedIndex
  2- Method which put the index selected into it --> selectAnswer()
  3- Submit & Next Button disabled until the answer has not been submitted
  4- Only Submit button enabled when an answer has been selected
  5- Only Next Button enabled when an answer has been submitted
  6- Method which verify if the selected Index is the right answer on clicking on Submit --> submitAnswer()
  7- Method which colorize the answers depends on if the answer has been selected or submitted (right or wrong)
    in order to let the user about his response. 


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
