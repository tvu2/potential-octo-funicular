# X-Team 37 Proposal for Developing a Kitchen Manager Application

## Goal

Work as a team to create a project proposal for your X-team to complete together.
The project does not have to be extremely difficult,
but there must be work to do for each member of your team.
You may reference figures using "See figure 1".  
Be sure to submit corresponding image files, i.e. figure1.png (or figure1.jpg) for each figure.

## Grading: To earn full credit, your team's proposal must include:

* (md) documentation: [this file] describing purpose and use of your program

* Description of a program that has:

  ** a main Java program class in a file named Main.java
  
  ** a custom data structure designed and built by your team
  
  ** comprehensive testing of individual units
  
 Caution: You are not being asked to implement this program, at least not yet. 
 We just want your group to make a proposal or pitch for your program.
 
 Tip: Your custom data structure can be composed of or extensions of data structures that you have learned and used in previous programming assignments.  We're looking for decisions about how to build a high-level data structure that will likely have lower-level components.

## Problem Description
1. Briefly describe a problem that your team would like to solve.  
The problem our team wants to solve is how to efficiently manage our kitchen supply such as dry ingredients, fresh/perishable ingredients so that we can avoid wasting them. 

2. Describe at a high level a program that could solve that problem.  
We propose to develop a kitchen manager application that allows users to edit(add, remove, update)/view the inventory (list of ingredients), edit/view the cookbook (list of recipes). The users can also select one or more recipes from the cookbook and the application would tell the users whether they have enough ingredients to execute the recipes. Furthermore, the application can suggest recipes for users based on available ingredients if the selected recipes can not be executed. These capabilities help sove the problem stated above in the following ways: 
* Users can view what ingredients they have and the expiration dates so when they do grocery shopping, they would not buy items that are still good and available at home. In other words, they can decide which ingredients should be used before they go bad. 
* Users can select from the suggested recipes to cook meals with available ingredients so these ingredients will be used up and not go to waste.


## Questions to answer for Exercise #2

1. Name: Give your project proposal a name (and edit the top line of this file)

Developing a Kitchen Manager Application

2. Output: Describe the output your program will produce.  Include and example format of the output produced.

Depending on the input data, the output can be different. Below is some examples of outputs produced by our Kitchen Manager Application

|Output format|Output description|Notes|
|---|---|---|
|Table/spreadsheet/csv file|List of all ingredients available in the inventory sorted by expiration date. Each ingredient comes with the following properties: name, description, category (eg. Meat, Vegetable, Dry,etc.), expiration date, purchased date, amount.|See file inventory.csv|
|Table/spreadsheet/csv file| List of ingredients needed for a particular recipe.|See recipe_list.csv|
|Text document/txt file| A recipe with required ingredients and instructions of how to execute it.|See recipe.txt|


3. Input: Describe the data that is needed to solve your problem. Include an example format of the input data.

Our program requires multiple data type, described in table below.

|Input format|Input description|Examples|  
|---|---|---|  
|String/text|Users' actions/requests|view inventory, update inventory, view recipe|  
|String/text|Description of a recipe|See reciple.txt|  
|String/text| Name, description of ingredients, units|Eggs, Pasta, Cheese, lbs, oz|
|Numbers|Inputs for ingredients' quantity, shelf life(by days)| 12, 3.5|
|Date|Inputs for expiration date, purchse date||Dec 13 2018|

4. User Interface: Describe a user interface for your program.  Use text menus or a simple graphic user interface.



5. Types List: Break your solution idea down into units that you think can be implemented with a single class.



Name each interface or class and briefly describe its function or purpose.


## Edit and Submit this file and any figures referenced by this document.

