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
  
  ** comprehensive testing of individual units **@lewisgross1296: can you work on this part?)**
  
 Caution: You are not being asked to implement this program, at least not yet. 
 We just want your group to make a proposal or pitch for your program.
 
 Tip: Your custom data structure can be composed of or extensions of data structures that you have learned and used in previous programming assignments.  We're looking for decisions about how to build a high-level data structure that will likely have lower-level components.

## Problem Description
1. Briefly describe a problem that your team would like to solve.  
The problem our team wants to solve is how to efficiently manage our kitchen supply such as dry ingredients, fresh/perishable ingredients so that we can avoid wasting them. 

2. Describe at a high level a program that could solve that problem.  
We propose to develop a kitchen manager application that allows users to edit(add, remove, update)/view the inventory (list of ingredients), edit/view the cookbook (list of recipes). The users can also select one or more recipes from the cookbook and the application would tell the users whether they have enough ingredients to execute the recipes. Furthermore, the application can suggest recipes for users based on available ingredients if the selected recipes can not be executed. These capabilities help sove the problem stated above in the following ways: 
* Users can view what ingredients they have so when they do grocery shopping, they can decide how many/much they need to buy. 
* Users can select from the suggested recipes to cook meals with available ingredients so these ingredients will be used up and not go to waste.


## Questions to answer for Exercise #2

1. Name: Give your project proposal a name (and edit the top line of this file)

Developing a Kitchen Manager Application

2. Output: Describe the output your program will produce.  Include and example format of the output produced.

Depending on the input data, the output can be different. Below is some examples of outputs produced by our Kitchen Manager Application

|Output format|Output description|Notes|
|---|---|---|
|Table/spreadsheet|List of all ingredients available in the inventory. Each ingredient comes with the following properties: ID, name, description, category (eg. Meat, Vegetable, Dry,etc.), quantity, units, location.|See file inventory.csv|
|Text document| A recipe with required ingredients and instructions of how to execute it.|See recipe.txt|

3. Input: Describe the data that is needed to solve your problem. Include an example format of the input data.

Our program requires multiple data type, described in table below.

|Input format|Input description|Examples|  
|---|---|---|  
|String/text|Users' actions/requests|view inventory, view ingredient, edit(add, remove, update) ingredient, view cookbook, view recipe, edit(add, remove, update) recipe|  
|String/text|Recipe's instruction|See recipe.txt|  
|String/text|Name, description, category, units, location of ingredients|Apples, Fuji, Fruits, counts, Fridge|
|Number|Inputs for ingredients' quantity|5|

4. User Interface: Describe a user interface for your program.  Use text menus or a simple graphic user interface.



5. Types List: Break your solution idea down into units that you think can be implemented with a single class.
	**a. KitchenManagerADT.java**
	This is the interface for the Kitchen Manager application. It has the following methods
	```
	public interface KitchenManagerADT {
		// This method returns the inventory as a hash table of ingredient objects. The ingredient object is comparable and used as a key. The Object represents the quantity of the Ingredient object in the inventory. It could be Integer or Double.
		public HashTable<Ingredient, Object> viewInventory();
		// This method adds a new ingredient to the inventory. It first checks if the ingredient exists in the inventory. If it exists in the inventory, it will update the inventory with new inputs. If it does not exists in the inventory, it will add the ingredient to the inventory. If the ingredient is null, it will throw an IllegalArgumentException.  
		public void addIngredient(Ingredient ingredient) throws IllegalArgumentException;
		// This method updates an existing ingredient in the inventory. It first checks if the ingredient exists in the inventory. If it does not exists, throws a NoSuchElementException. If the ingredient is null, it throws an IllegalArgumentException. If the ingredient exists, it update the ingredient with new properties.  
		public void updateIngredient(Ingredient ingredient) throws IllegalArgumentException, NoSuchElementException;
		// This method removes an existing ingredient in the inventory. It checks if the ingredient exists. It throws exceptions similar to updateIngredient method. If the ingredient exists, it remove the ingredient from the inventory. 
		public void removeIngredient(Ingredient ingredient);
		// This method return an ingredient object. If the ingredient doesn't exist in the inventory or is null, it throws NoSuchElementException or IllegalArgumentException respectively. 
		public Ingredient viewIngredient(Ingredient ingredient) throws IllegalArgumentException, NoSuchElementException;
		// This method returns the cookbook as a list of recipe objects.
		public List<Recipe> viewCookBook();
		// This method adds a new recipe to the cookbook. If the recipe exists in the cookbook, it will update the recipe. Otherwise it will add the recipe. It throws an IllegalArgumentException if the recipe is null. 
		public void addRecipe(Recipe recipe) throws IllegalArgumentException;
		// This method updates an existing recipe in the cookbook. If the recipe exists, it will update the recipe with new properties. Otherwise, it will throw a NoSuchElementException. If the recipe is null, it throws IllegalArgumentException. 
		public void updateRecipe(Recipe recipe) throws IllegalArgumentException, NoSuchElementException;
		// This method removes an existing recipe in the cookbook. If the recipe exists, it will remove the recipe from the cookbook. Otherwise, it will throw a NoSuchElementException. If the recipe is null, it throws an IllegalArgumentException
		public void removeRecipe(Recipe recipe) throws IllegalArgumentException, NoSuchElementException;
		// This method returns a recipe object. If the recipe does not exist or is null, it will throw NoSuchElementException or IllegalArgumentException respectively. 
		public Recipe viewRecipe(Recipe recipe) throws IllegalArgumentException, NoSuchElementException;
	} 
	```
	**b. KitchenManager.java**
	This class implements the methods described in the KitchenManagerADT.java
	```
	public class KitchenManager(){
		// Constructor to create a KitchenManager object
		KitchenManager() {};
		// In addition to the public methods described in the KitchenManagerADT.java, it may have additional private helper methods such as methods to load inventory from file on disk or database, save inventory to file after update, etc. 
	}
	```
	**c. Ingredient.java** 
	This class represents ingredient. 
	```
	public class Ingredient() {
		private String name, description, category, location, unit;
		// Constructor to create an Ingredient object
		Ingredient(String name, String description, String category, String unit, String location) {}
		// Accessor methods
		// Mutator methods
		// Overide equals() method to compare two ingredients object. If they have the same name, and description, they are the same object
		@overide
		public int equals(Ingredient ingredient){}
		// Overide hashCode method
		@overide
		public int hashCode(Ingredient ingredient){}
	}
	```
	**d. Recipe.java**
	This class represents recipe
	```
	public class Recipe() {
		private String name; // name of the recipe
		private List<Ingredient>; // list of ingredients
		private List<Object>; // list of quantities (numbers can be integer or double)
		private String instruction; // instruction how to execute the recipe
		// Constructor
		Recipe(List<Ingredient> ingredients, List<Object> quantities, String instruction)
		// Accessor methods
		// Mutator methods
		// Overide equals() method to compare two recipes. If they have the same name, same List of ingredients, they are the same.
		@overide
		public boolean equals(Recipe recipe) {}
	}
	```

	**e. Main.java**
   	This class takes in users' inputs and processes them by calling appropriate KitchenManager methods.  
   	```
   	public main() {
   	// Create a KitchenManager object
   	KitchenManger KM = new KitchenManager();
   	// Ask users to select one of the 10 actions: view inventory, view ingredient, add ingredient, update ingredient, remove ingredient, view cookbook, view recipe, add recipe, update recipe, remove recipe
   	// Depending on the action, the users may need to provide more information (recipe or ingredient) and the KitchenManager will calls appropriate method to execute the action
   	// Some user interface methods to display data for user or get inputs from users
   }
   ```

## Edit and Submit this file and any figures referenced by this document.

