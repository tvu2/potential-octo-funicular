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
  
  ** comprehensive testing of individual units **@lewisgross1296: can you work on this part?**
  
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

Depending on the input data, the output can be different. Below is some examples of outputs produced by our Kitchen Manager Application: 
* List of all ingredients in the inventory (inventory.csv). 
* Detail of an ingredient with the following properties: ID, name, description, category (eg. Meat, Vegetable, Dry,etc.), quantity, units, location (Room, Freezer, Fridge).
* List of all recipes in the cookbook.
* Detail of a recipe with name, list of ingredients, the required quantities, and instruction how to make the recipe. 

3. Input: Describe the data that is needed to solve your problem. Include an example format of the input data.

Our program requires multiple data type, below are some examples:
* List of actions: view inventory/cookbook, add ingredient/recipe, edit ingredient/recipe, delete ingredient/recipe, make recipe. 
* Ingredient inputs: name (eg. Apple), description (eg. Fuji), category (eg. Fruit), quantity (eg. 3), unit (eg. counts), location (eg. Fridge).
* Recipe inputs: name, lists of ingredients and corresponding quantities, instruction  

4. User Interface: Describe a user interface for your program.  Use text menus or a simple graphic user interface.

The program will contain two main screens that the user can select from. The first screen (see inventory.jpg) will be the Inventory screen. From here the user can create, delete, edit, and view individual ingredients. To change the properties of an ingredient the user will click the Edit button. From there a new window will pop up with additional details such as a description of the ingredient and the quantity (which can be changed as needed). The View button will take the user to a similar window as the Edit button, except all fields will be uneditable. To create a brand new ingredient the user will click the Add New Ingredient button. To delete an ingredient, user will click the delete button, and the ingredient will be removed from the inventory.

![Inventory Screen](https://github.com/tvu2/potential-octo-funicular/blob/TV_branch/inventory.jpg)

The second screen (see cookbook.jpg) in the program will be the Cookbook screen. In the Cookbook screen the user can manage recipes made up of one or more ingredients. The View, Edit, Delete and Add New Recipe buttons in the Cookbook screen have similar functionalities as those in the Inventory screen. The Make button will take the user to another screen where the recipe ingredients will be listed (ingredients that are missing will be listed in red). If all ingredients are available, the user can confirm they want to make the recipe, which will automatically subtract all ingredients used in the Inventory menu.

![Cookbook Screen](https://github.com/tvu2/potential-octo-funicular/blob/TV_branch/cookbook.jpg)

5. Types List: Break your solution idea down into units that you think can be implemented with a single class.

	**a. KitchenManagerADT.java**
	This is the interface for the Kitchen Manager application.
	```
	public interface KitchenManagerADT {
		// This method returns the inventory as a hash table of ingredient objects. 
		// The Ingredient object is comparable and used as a key. 
		// The Object represents the quantity of the Ingredient object. It could be Integer or Double.
		
		public HashTable<Ingredient, Object> viewInventory();
		
		// This method adds a new ingredient to the inventory. 
		// It first checks if the ingredient exists in the inventory. 
		// If it exists in the inventory, it will update the inventory with new inputs. 
		// If it does not exists in the inventory, it will add the ingredient to the inventory. 
		// If the ingredient is null, it will throw an IllegalArgumentException.  
		
		public void addIngredient(Ingredient ingredient) throws IllegalArgumentException;
		
		// This method updates an existing ingredient in the inventory. 
		// It first checks if the ingredient exists in the inventory. 
		// If it does not exists, throws a NoSuchElementException. 
		// If the ingredient is null, it throws an IllegalArgumentException. 
		// If the ingredient exists, it update the ingredient with new properties.  
		
		public void updateIngredient(Ingredient ingredient) throws IllegalArgumentException, NoSuchElementException;
		
		// This method removes an existing ingredient in the inventory. 
		// It checks if the ingredient exists. 
		// It throws exceptions similar to updateIngredient method. 
		// If the ingredient exists, it remove the ingredient from the inventory. 
		
		public void removeIngredient(Ingredient ingredient) throws IllegalArgumentException, NoSuchElementException;
		
		// This method returns an ingredient object. 
		// It throws exceptions similar to updateIngredient method

		public Ingredient viewIngredient(Ingredient ingredient) throws IllegalArgumentException, NoSuchElementException;

		// This method returns the cookbook as a list of recipe objects.
		
		public List<Recipe> viewCookBook();

		// This method adds a new recipe to the cookbook. 
		// If the recipe exists in the cookbook, it will update the recipe. 
		// Otherwise it will add the recipe. 
		// It throws an IllegalArgumentException if the recipe is null. 
		
		public void addRecipe(Recipe recipe) throws IllegalArgumentException;
		
		// This method updates an existing recipe in the cookbook. 
		// If the recipe exists, it will update the recipe with new properties. 
		// Otherwise, it will throw a NoSuchElementException. 
		// If the recipe is null, it throws IllegalArgumentException. 
		
		public void updateRecipe(Recipe recipe) throws IllegalArgumentException, NoSuchElementException;
		
		// This method removes an existing recipe in the cookbook. 
		// It throws similar exceptions to updateRecipe method. 

		public void removeRecipe(Recipe recipe) throws IllegalArgumentException, NoSuchElementException;
		
		// This method returns a recipe object. 
		// It throws similar exceptions to updateRecipe method. 

		public Recipe viewRecipe(Recipe recipe) throws IllegalArgumentException, NoSuchElementException;

		// This method makes the recipe.
		// It reduces the ingredients in the inventory by the quantites used in the recipe
		// It throws similar exceptions to the updateRecipe method

		public void makeRecipe(Recipe recipe) throws IllegalArgumentException, NoSuchElementException;
	} 
	```
	**b. KitchenManager.java**
	This class implements the methods described in the KitchenManagerADT.java
	```
	public class KitchenManager(){
		// Constructor to create a KitchenManager object
		KitchenManager() {};
		// Implementation Public methods listed in KitchenManagerADT.java
		// Additional private helper methods such as: 
		// load/read inventory from file on disk, save inventory to file after update, etc. 
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
		// Overide equals() method to compare two ingredients object using the following rule: 
		// If they have the same name, and description, they are the same ingredients
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
		// Overide equals() method to compare two recipes. 
		// If they have the same name, same List of ingredients, they are the same recipes.
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
   	// Display options for users to select: 
	// view inventory/cookbook, view ingredient/recipe, 
	// edit ingredient/recipe, delete ingredient/recipe, add ingredient/recipe, make recipe.
   	// Depending on the selected action, the users may need to provide more information (recipe or ingredient) 
	// and the KitchenManager will calls appropriate method to execute the action
   	// Some user interface methods to display data for user or get inputs from users
   }
   ```

## Edit and Submit this file and any figures referenced by this document.

