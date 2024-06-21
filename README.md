# python-project-for_internship
python-project-for_-internship
Acknowledgement
You’ll start by creating a basic Python quiz application that’s only capable of asking a question, collecting an answer, and checking whether the answer is correct. From there, you’ll add more and more features in order to make your app more interesting, user-friendly, and fun.

You’ll build the quiz application iteratively by going through the following steps:

*Create a basic application that can ask multiple-choice questions.

*Make the app more user-friendly by improving how it looks and how it handles user errors.

*Refactor the code to use functions.

*Separate question data from source code by storing questions in a dedicated data file.

*Expand the app to handle multiple correct answers, give hints, and provide explanations.

*Add interest by supporting different quiz topics to choose from.

#Prerequisites

In this tutorial, you’ll build a quiz application using Python’s basic building blocks. While working through the steps, it’s helpful if you’re comfortable with the following concepts:

*Reading input from the user at the terminal

*Organizing data in structures like lists, tuples, and dictionaries

*Using if statements to check different conditions

*Repeating actions with for and while loops

*Encapsulating code with functions

If you’re not confident in your knowledge of these prerequisites, then that’s okay too! In fact, going through this tutorial will help you practice these concepts. You can always stop and review the resources linked above if you get stuck.

#Use Lists and Tuples to Avoid Repetitive Code

Python provides several flexible and powerful data structures. You can usually replace repeated code with a tuple, a list, or a dictionary in combination with a for loop or a while loop.

Instead of repeating code, you’ll treat your questions and answers as data and move them into a data structure that your code can loop over. The immediate—and often challenging—question then becomes how you should structure your data.

There’s never one uniquely perfect data structure. You’ll usually choose between several alternatives. Throughout this tutorial, you’ll revisit your choice of data structure several times as your application grows.

For now, choose a fairly simple data structure:

*A list will hold several question elements.

*Each question element will be a two-tuple consisting of the question text and the answer.

#Provide Multiple Choices

Here, the alternatives show that you expect the answer to be entered without parentheses. In the example, the alternatives are listed before the question. This is a bit counterintuitive, but it’s easier to implement into your current code. You’ll improve this in the next step.

In order to implement answer alternatives, you need your data structure to be able to record three pieces of information for each question:

*The question text *The correct answer *Answer alternatives

It’s time to revisit QUESTIONS for the first—but not the last—time and make some changes to it. It makes sense to store the answer alternatives in a list, as there can be any number of them and you just want to display them to the screen. Furthermore, you can treat the correct answer as one of the answer alternatives and include it in the list, as long as you’re able to retrieve it later.

You decide to change QUESTIONS to a dictionary where the keys are your questions and the values are the lists of answer alternatives. You consistently put the correct answer as the first item in the list of alternatives so that you can identify it.

#Keep Score

Now that you’re numbering the questions, it would also be nice to keep track of how many questions the user answers correctly. You can add a variable, num_correct, to take care of this: You increase num_correct for each correct answer. The num loop variable already counts the total number of questions, so you can use that to report the user’s result.

#Handle User Errors

So far, you haven’t worried too much about what happens if the user enters an answer that’s not valid. In the different versions of your app, this oversight could result in the program raising an error or—less dramatically—registering a user’s invalid answer as wrong.

You can handle user errors in a better way by allowing the user to re-enter their answer when they enter something invalid. One way to do this is to wrap input() in a while loop:

The condition (text := input()) != "quit" does a few things at once. It uses an assigment expression (:=), often called the walrus operator, to store the user input as text and compare it to the string "quit". The while loop will run until you type quit at the prompt. See The Walrus Operator: Python 3.8 Assignment Expressions for more examples.

#Note: If you’re using an older version of Python than 3.8, then the assignment expression will cause a syntax error. You can rewrite the code to avoid using the walrus operator. There’s a version of the quiz application that runs on Python 3.7 in the source code that you downloaded earlier.

#Add Variety to Your Quiz

Currently, when you run your quiz application, you’re always asking the questions in the same order as they’re listed in your source code. Additionally, the answer alternatives for a given question also come in a fixed order that never changes.

You can add some variety to your quiz by changing things up a little. You can randomize both the order of the questions and the order of the answer alternatives for each question:

You use random.sample() to randomize the order of your questions and the order of the answer alternatives. Usually, random.sample() picks out a few random samples from a collection. However, if you ask for as many samples as there are items in the sequence, then you’re effectively randomly reordering the whole sequence:

Additionally, you cap the number of questions in the quiz to NUM_QUESTIONS_PER_QUIZ which is initially set to five. If you include more than five questions in your application, then this also adds some variety as to which questions get asked in addition to the order in which they’re asked.

#Note: You can also use random.shuffle() to shuffle your questions and alternatives. The difference is that shuffle() reorders sequences in place, which means that it changes your underlying QUESTIONS data structure. sample() creates new lists of questions and alternatives, instead.

In your current code, using shuffle() wouldn’t be a problem because QUESTIONS is reset every time you run your quiz application. It could become a problem down the line, for example if you implement the possibility of asking the same question several times. Your code is usually simpler to reason about if you don’t change or mutate your underlying data structure.

Throughout this step, you’ve improved on your quiz application. It’s now time to take a step back and consider the code itself. In the next section, you’ll reorganize the code so that you keep it modular and ready for further development.

#Organize Your Code With Functions

In this step, you’ll refactor your code. Refactoring means that you’ll change your code, but your application’s behavior and your user’s experience will stay as they are. This may not sound very exciting, but it’ll be tremendously useful down the line, as good refactorings make it more convenient to maintain and expand your code.

#Note: If you’d like to see two Real Python team members work through refactoring some code, then check out Refactoring: Prepare Your Code to Get Help. You’ll also learn how to ask clear, concise programming questions.

Currently, your code isn’t particularly organized. All your statements are fairly low level. You’ll define functions to improve your code. A few of their advantages are the following:

Functions name higher-level operations that can help you get an overview of your code. Functions can be reused.

#Prepare Data

Many games and applications follow a common life cycle:

*Preprocess: Prepare initial data.

*Process: Run main loop.

*Postprocess: Clean up and close application.

In your quiz application, you first read the available questions, then you ask each of the questions, before finally reporting the final score. If you look back at your current code, then you’ll see these three steps in the code. But the organization is still a bit hidden within all the details.

You can make the main functionality clearer by encapsulating it in a function. You don’t need to update your quiz.py file yet, but note that you can translate the previous paragraph into code that looks like this:

This code won’t run as it is. The functions prepare_questions() and ask_question() haven’t been defined, and there are some other details missing. Still, run_quiz() encapsulates the functionality of your application at a high level.

Writing down your application flow at a high level like this can be a great start to uncover which functions are natural building blocks in your code. In the rest of this section, you’ll fill in the missing details:

*Implement prepare_questions().

*Implement ask_question().

*Revisit run_quiz().

You’re now going to make quite substantial changes to the code of your quiz application as you’re refactoring it to use functions. Before doing so, it’s a good idea to make sure you can revert to the current state, which you know works. You can do this either by saving a copy of your code with a different filename or by making a commit if you’re using a version control system.

Note that prepare_questions() deals with general questions and num_questions parameters. Afterward, you’ll pass in your specific QUESTIONS and NUM_QUESTIONS_PER_QUIZ as arguments. This means that you don’t depend on global variables in your function. With this decoupling, your function is more general, and you can later more readily replace the source of your questions.

#Ask Questions

Look back on your sketch for the run_quiz() function and remember that it contains your main loop. For each question, you’ll call ask_question(). Your next task is to implement that helper function.

Think about what ask_question() needs to do:

*Pick out the correct answer from the list of alternatives

*Shuffle the alternatives

*Print the question to the screen

*Print all alternatives to the screen

*Get the answer from the user

*Check that the user’s answer is valid

*Check whether the user answered correctly or not

*Add 1 to the count of correct answers if the answer is correct

These are a lot of small things to do in one function, and you could consider whether there’s potential for further modularization. For example, items 3 to 6 in the list above are all about interacting with the user, and you can pull them into yet another helper function.

You first randomly reorder the answer alternatives using random.shuffle(), as you did earlier. Next, you call get_answer(), which handles all details about getting an answer from the user. You can therefore finish up ask_question() by checking the correctness of the answer. Observe that you return 1 or 0, which indicates to the calling function whether the answer was correct or not.

As earlier, you use enumerate() to keep a counter that numbers the questions you ask. You can increment num_correct based on the return value of ask_question(). Observe that run_quiz() is your only function that directly interacts with QUESTIONS and NUM_QUESTIONS_PER_QUIZ.

Your refactoring is now complete, except for one thing. If you run quiz.py now, then it’ll seem like nothing happens. In fact, Python will read your global variables and define your functions. However, you’re not calling any of those functions. You therefore need to add a function call that starts your application:

Separate Data Into Its Own File
You’ll continue your refactoring journey in this step. Your focus will now be how you provide questions to your application.

So far, you’ve stored the questions directly in your source code in the QUESTIONS data structure. It’s usually better to separate your data from your code. This separation can make your code more readable, but more importantly, you can take advantage of systems designed for handling data if it’s not hidden inside your code.

In this section, you’ll learn how to store your questions in a separate data file formatted according to the TOML standard. Other options—that you won’t cover in this tutorial—are storing the questions in a different file format like JSON or YAML, or storing them in a database, either a traditional relational one or a NoSQL database.

#Expand Your Quiz Functionality

In this fifth step, you’ll add more functionality to your quiz application. Finally, the refactoring you’ve done in the previous steps will pay off! You’ll add the following features:

*Questions with multiple correct answers

*Hints that can point toward the correct answer

*Explanations that can act as teaching moments

#MULTIPLE CHOICE IMAGE



![multiple](https://github.com/vishnuyadav78/python-project-for_internship/assets/173454005/a9f9b97b-0948-4640-8eab-f4ff66eb65a2) 



DEMO IMAGE OF SOURCE CODE



B![H](https://github.com/vishnuyadav78/python-project-for_internship/assets/173454005/0a3b9723-b5d0-4f57-af2b-0f8f759adf7d)





![B](https://github.com/vishnuyadav78/python-project-for_internship/assets/173454005/359b89e0-aab4-44aa-8b4e-155adf9ec110)
