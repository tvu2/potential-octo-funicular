# X-Team 37 Proposal for Developing a Kitchen Manager Application

## Problem Description
The problem our team wants to solve is how to efficiently manage our kitchen supply so that we don't keep buying ingredients that we already have in the kitchen. 

To solve this problem, we propose to develop a kitchen manager application that allows users to create an inventory which essentially a collections of ingredients and their quantities. Users can make changes to the inventory by adding new ingredients, deleting existing ingredients, or editing ingredients properties and quantities. Similarly, users can create a cookbook, which is a collection of recipes. They can add/remove/edit recipes. The users can also select one or more recipes from the cookbook and the application would tell the users whether they have enough ingredients to execute the recipes. With these capabilities, users can view what ingredients they have so when they do grocery shopping, they can decide how many/much they need to buy. Furthermore, because users can select from the available recipes to cook meals with available ingredients, these ingredients will be used up and not go to waste.

## Description of the Kitchen Manager Application
Our program will consist of the classes and interface in the table below. Detail of these are presented in answer to question 5 of the section below.  

|Name|Description|File|
|---|---|---|
|Main|This class takes in users' inputs and processes them by calling appropriate KitchenManager methods.|Main.java|
|KitchenManagerADT|This is the interface for the Kitchen Manager application.|KitchenManagerADT.java|
|KitchenManager|This class implements the methods described in the interface.|KitchenManager.java|
|Ingredient|This class represent an ingredient object.|Ingredient.java|
|Recipe|This class represents a recipe object.|Recipe.java|

Our custom objects are Ingredient, and Recipe. We use a hash table (similar to assignment P3) to store the inventory with Ingredient being the key and quantity being the value. Since Ingredient is a custom object, we need to overide the equals and hashCode methods to support hash table operations. For a cookbook which is a collection of recipes, we used List to store the recipes. Since Recipe is also a custom object, we also need to overide the equals method to support List operations. 

Besides the program described above, we will also develop a comprehensive test suit to thoroughly test all the functionalities of our application. Since we are developing the program, we have access to all the code, we are conducting a white unit testing to cover all path of the codes: public methods, private helper methods, user interface methods. We will use JUnit test framework to write our test cases. Some example of test cases are provided as part of answer to question 5 in the section below. 


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

![Inventory Screen](https://github.com/tvu2/potential-octo-funicular/blob/master/inventory.jpg)

The second screen (see cookbook.jpg) in the program will be the Cookbook screen. In the Cookbook screen the user can manage recipes made up of one or more ingredients. The View, Edit, Delete and Add New Recipe buttons in the Cookbook screen have similar functionalities as those in the Inventory screen. The Make button will take the user to another screen where the recipe ingredients will be listed (ingredients that are missing will be listed in red). If all ingredients are available, the user can confirm they want to make the recipe, which will automatically subtract all ingredients used in the Inventory menu.

![Cookbook Screen](https://github.com/tvu2/potential-octo-funicular/blob/master/cookbook.jpg)

5. Types List: Break your solution idea down into units that you think can be implemented with a single class.

	**a. KitchenManagerADT.java**
	This is the interface for the Kitchen Manager application. Here are examples of a couple of main functionalities of the application. We anticipate to add more methods in later development stages. 
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

		// Returns a lists of all ingredient objects currently inside of the Inventory.
		public List<Ingredient> viewIngredients();

		// Returns a list of all recipe objects currently inside of the Cookbook.
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
	This class implements the methods described in the interface KitchenManagerADT.java.
	```
	public class KitchenManager(){
		// Constructor to create a KitchenManager object
		KitchenManager() {};
		// Implementation Public methods listed in KitchenManagerADT.java
		// Additional helper methods such as: 
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
		// Additional helper methods
	}
	```
	**d. Recipe.java**
	This class represents recipe.
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
		// Additional helper methods
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
	**f. TestSuite.java**
	This class is responsible for testing the implementation of all classes with the JUnit framework
	
	```
	import org.junit.Assert.*;
	import org.junit.Test;
	public class TestSuite{
	
		@Test
		public void test01isEmptyCB() {
		// Checks to see if a cookbook with no recipes is empty
		}
	
		@Test
		public void test02isEmptyInv() {
		// Checks to see if an inventory with no ingredients is empty
		}
	
		@Test
		public void test03addIngredients() {
		// Initialize some ingredient objects
		// Add these ingredients to the cookbook
		// Run viewIngredients() and iterate through the hash table to make sure all ingredient objects created are
		// in the table
		}
		
		@Test
		public void test04addRecipes() {
		// Initialize some recipe objects
		// Add these ingredients to the cookbook
		// Run viewcookbook() and iterate through list to make sure all recipe objects created are
		// in the List		
		}
		
		@Test
		public void test05ingredientUpdates() {
		// Create an ingredient
		// Call the updateIngreedient method
		// compare the ingredient found in the hash table with the updated data
		// to make sure they are the same
		}
		
		@Test
		public void test06recipeUpdates() {
		// Create a recipe
		// Call the updateRecipe method
		// compare the recipe found in the hash table with the updated data
		// to make sure they are the same		}
		
		@Test
		public void test07removeIngredient() {
		// Add an Ingredient, remove it from the hashTable and call viewIngredient() method
		// The test should throw a NoSuchElementException. 
		}
		
		@Test
		public void test08removeRecipe() {
		// Add a recipe, remove it from the hashTable and call viewRecipe() method
		// The test should throw a NoSuchElementException
		}
		
		@Test
		public void test09AddManyIngredients() {
		// Initialize/add many ingredients to the cookbook
		// Run through all ingredients to make sure they are all there
		}
		
		@Test
		public void test10AddManyRecipes() {
		// Initialize/add many recipes to the cookbook
		// Run through all recipes to make sure they are there
		}
		
		@Test
		public void test11MakeRecipeUpdateInventory() {
		// Initialize and add many ingredients to the cookbook
		// with a certain quantity.
		// Initialize and add a custom recipe.
		// call makeRecipe() method and then viewInventory() to check if the quantity has been updated
		}
		
		@Test
		public void test12IngredientQuantityUnderZero() {
		// Test the special/error case where an ingredient's quantity may
		// drop below zero.
		}
		
		@Test 
		public void test13ViewNullRecipe() {
		// Test to see if viewRecipe() throws an exception when
		// attempting to view a null recipe argument.
		}
		
		@Test 
		public void test14RemoveNullRecipe() {
		// Test to see if removeRecipe() throws an exception when
		// attempting to remove a null recipe argument.
		}
		
		@Test 
		public void test15RemoveRecipeFromEmptyBook() {
		// Test to see if removeRecipe() throws an exception when
		// attempting to remove a recipe in an empty cookbook.
		}
		
		@Test 
		public void test16RemoveRecipeNotInBook() {
		// Initialize some recipes into cookbook.
		// Test to see if removeRecipe() throws an exception when
		// attempting to remove a recipe that is not in the cookbook.
		}
		
		// Similar tests to test14-test16 can be written for updateRecipe(), 
		// makeRecipe() and viewRecipe(). 
		
		// More test cases
	}
	```
