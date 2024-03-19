**1. Problem Statement of the App:**

The Quiz App is a web application that provides users with an interactive quiz experience. 
Users can test their knowledge on various web development topics by answering multiple-choice questions within a limited time frame.
Once the quiz is started, the user can't exit the quiz until they complete it.
When the time runs out on a question, the answer is automaitcally given and the user must move on to the next question.
Each question is kept track off at the bottom left of the screen, so the user doesn't get lost. 
At the end of the quiz, the user is given their score and have the option of quiting or restarting the quiz.
The app aims to engage users in an enjoyable learning activity while providing instant feedback on each question.

**2. Functional Features of the App:**

- Start Quiz Button: Allows users to initiate the quiz.

  // select the .start_btn element from the html file.
  const start_btn = document.querySelector(".start_btn button");

  // if startQuiz button clicked
  start_btn.addEventListener("click", (e) => {
    info_box.classList.add("activeInfo"); //show info box
  });

- Timer: Displays a countdown timer for each question.

  // control the timer and actions associated to it
  function startTimer(time) {
    counter = setInterval(timer, 1000);
    function timer() {
      timeCount.textContent = time; //change the value of timeCount with time value
      time--; //decrement the time value
      if (time < 9) {
        //if timer is less than 9
        let addZero = timeCount.textContent;
        timeCount.textContent = "0" + addZero; //add a 0 before time value
      }
  // marks the correct answer if the timer runs out
   if (time < 0) {
        //if timer is less than 0
        clearInterval(counter); //clear counter
        timeText.textContent = "Time Off"; //change the time text to time off
          const allOptions = option_list.children.length; //get all option items
          let correcAns = questions[que_count].answer; //get correct answer from array
          for (i = 0; i < allOptions; i++) {
            if (option_list.children[i].textContent == correcAns) {
              //if there is an option which is matched to an array answer
              option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
              option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
              console.log("Time Off: Auto selected correct answer.");
            }
          }
    
- Question Display: Presents questions one at a time with multiple-choice options.

    // getting questions and options from array
  // If you have lesser or more number of options you need to change this code
  function showQuetions(index) {
    const que_text = document.querySelector(".que_text");
  
    //creating a new span and div tag for question and option and passing the value using array index
    // self exercise: re-write the following using backtick syntax for string in JS instead of concatenation operator
    let que_tag =
      "<span>" +
      questions[index].numb +
      ". " +
      questions[index].question +
      "</span>";
    let option_tag =
      '<div class="option"><span>' +
      questions[index].options[0] +
      "</span></div>" +
      //...copy and paste the code for the remaining questions.

- Option Selection: Enables users to select an answer from the provided options.

  //if user clicked on option
  function optionSelected(answer) {
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    let userAns = answer.textContent; //getting user selected option
    let correcAns = questions[que_count].answer; //getting correct answer from array
    const allOptions = option_list.children.length; //getting all option items

- Feedback: Provides immediate feedback on the correctness of the chosen answer.

  //if user selected option is equal to array's correct answer
  if (userAns == correcAns) {
    userScore += 1; //update total score value increment by 1
    answer.classList.add("correct"); //add green color to correct selected option
    answer.insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to correct selected option
    console.log("Correct Answer");
    console.log("Your correct answers = " + userScore);
  } else {
    answer.classList.add("incorrect"); //add red color to correct selected option
    answer.insertAdjacentHTML("beforeend", crossIconTag); //add cross icon to correct selected option
    console.log("Wrong Answer");

- Score Tracking: Keeps track of the user's score based on correct answers.

  function showResult() {
  info_box.classList.remove("activeInfo"); //hide info box
  quiz_box.classList.remove("activeQuiz"); //hide quiz box
  result_box.classList.add("activeResult"); //show result box
  const scoreText = result_box.querySelector(".score_text");
  if (userScore > 3) {
    // if user scored more than 3
    //create a new span tag and pass the user score number and total question number
    let scoreTag =
      "<span>and congrats! , You got <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag; //add new span tag inside score_Text
  }
  //...see code base for the rest of this if conditional statement.

- Next Question Button: Allows users to proceed to the next question.

  // if Next Question button is clicked
  next_btn.addEventListener("click", (e) => {

- Exit Quiz Button: Enables users to exit the quiz at any time.

  // if exitQuiz button clicked
  exit_btn.addEventListener("click", (e) => {
    info_box.classList.remove("activeInfo"); //hide info box
  });

- Restart Quiz Button: Allows users to restart the quiz after completion.

  // if restartQuiz button clicked
  restart_quiz.addEventListener("click", (e) => {
    quiz_box.classList.add("activeQuiz"); //show quiz box
    result_box.classList.remove("activeResult"); //hide result box
    // ...see code base for the rest of restart button functionality.
  

**3. Explanation of the Directory Structure/Setup of the App:**

The Quiz App directory structure consists of the following files:

- **index.html:** This file contains the HTML structure of the web page, including elements for displaying questions, options, timer, and score.
- **style.css:** The CSS file responsible for styling the HTML elements to provide an aesthetic and symmetrical interface.
- **questions.js:** JavaScript file containing an array of quiz questions, along with their options and correct answers.
- **quizApp.js:** JavaScript file containing the main logic and functionality of the Quiz App, including question rendering, option selection, timer management, and the score calculation.

These files are linked together in the `head` section of the HTML file using `link` tags for CSS and internal `script` tags for JavaScript. 

**4. Explanation of the Codebase in Relevant Files:**

- **index.html:**
  - Defines the structure of the quiz interface using HTML elements such as `div`, `button`, `span`, and `footer`.
  - Includes links to external CSS and JavaScript files using `link` and `script` tags.
  - Provides placeholders for dynamic content such as questions, options, timer, and score.

- **style.css:**
  - Contains CSS rules for styling various elements of the quiz interface, including fonts, colors, layout, and animations.
  - Utilizes classes and IDs to target specific elements and apply styling rules.
  - Implements media queries for responsiveness and adaptability across different screen sizes.

- **questions.js:**
  - Defines an array of JavaScript objects, each representing a quiz question.
  - Each object contains properties such as question number, question text, options array, and correct answer.
  - The array serves as a data source for generating questions and options in the quiz interface.

- **quizApp.js:**
  - Implements the main logic and functionality of the Quiz App.
  - Includes functions for rendering questions and options, handles the option selection, managing the timer, and calculating the user's score.
  - Updates the quiz interface dynamically based on the user's choices.
  - Handles user input validation and provides immediate feedback on answer correctness.

This breakdown provides a comprehensive overview of the structure and functionality of the Quiz App, allowing beginners to understand how the different components work together to create an interactive quiz.
