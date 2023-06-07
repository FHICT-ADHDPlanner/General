# Recommendations

This document will outline the recommendations given for this project. These are things that were not implemented due to time constraints. 

## Application UI
This chapter will highlight the changes that would be recommended for the user interface.

### Colors
Colors are an important part of our lives and as figured out in the [research about ADHD](./Researches/ADHD%20and%20Project%20management.md), it has a great influence on the way people perceive things and how it motivates them. 

This is the reason the following user story was made:
- As a user, I want to have the ability to select the color scheme for the application because I want to choose what works best for me.

The recommendation is to make at least three color schemes, light, dark and custom. In addition to this, the option to changes the colors of tasks could be added. This makes it easier to see what task belongs to what category. 

### Showing subtasks
There is currently not a way to see the subtasks that were made. This is a vital part of the subtasks. 

The following user story was made:
- As a user I want to be able to fold out a task to see the subtasks so I can see what stills needs to happen to fully finish that task.

The recommendation is that a dropdown will be made within the task details. By clicking this, the subtasks become visible and will be able to be ticked off.

### Checking off (sub)tasks
Going further on the last recommendation, there is no option yet to check off a checkbox to show that a subtask or task is done. This could help in making it visible what still needs to be done and what is already done. In addition to this the task should be stricken through to show that it is done without clicking on the details.

This has the following user story:
- As a user, I want to be able to check off a checkbox when a task is done and also see this visually by striking through the name of the task. 

The recommendation is that there should be a checkbox added to the detail modal of the task and next to the subtasks. This way the user can check the checkbox and show that the task is done by the program also striking it through. 

### Progress bar
When a task has subtasks, these are not always visible. To make this more visible, it is possible to make a progress bar under the task or show the number of total subtasks next to the number of completed subtasks. 

The relating user story is:
- As a user, I want to be able to keep track of how far my subtasks are by seeing a bar under the main task because this will keep me motivated.

The recommendation is to give the user a visual representation of the subtasks in the form of a progress bar under the related task. The more subtasks are checked off, the more the progress bar fills. 

### Styling modals
The styling of the modals has taken a backseat while other tasks took priority. This is however something that could be worked on in the future. The styling now is the basic styling that React provides on new components.

## Functionality recommendations
This chapter will go into the recommendations for functionalities that could be added to the application.

### Friendship
Most people with ADHD get motivated by competition. This is where the friendship function comes in. This comes with a few different recommendations:

#### **Adding friends**

The first step is adding friends to your account. This can be done by making a search function where they can find their friends and click an add button. On the receiving end of this, the user getting a friend request will need a button to either accept or decline the request. 

The user story will be:
- As a user, I want to be able to send and accept/reject a friend request because I want to add friends.

The recommendation is then to add a search function with an add button. This does mean that on the receiving end, there should be an accept and reject button. 

#### **Friend list**
  
Another feature that should be added in the realm of friendship, is a friend list. There are multiple options on how to show this. It should at least show the amount of tasks completed to get that element of competition in. More will be explained later in the specific feature.

The user story of this would be:
- As a user, I want to be able to see my friends in a list because then I can see who my friends are.

The recommendation is to put this list of friends in a side panel next to the calendar to keep people motivated to use it and to keep on track with their tasks. 

#### **Friends task tracking**
  
Within the friends list there should be a feature that shows their progress in the tasks of the day. This is a feature that a user should be able to turn off so others can not see their progress.

The following user story was made:
- As a user, I want to be able to see the progress of tasks for my friends so I can be motivated to complete my own, furthermore I want to be able to turn this off.

