# Cook Book Documentation

## Backend

### Features

* User Authentication
  * Google Authentication + JWT

#### Types

```typescript
interface RecipeQueryFilter{
	type: string;
	val: string[] | string | number;
}
```

#### Routes

```typescript
getRecentRecipes()//returns recently created or used recipes

//should getRecipes and variations only display enough for some display and not whole recipe
//entire recipe could be accessed upon selection of a particular recipe
//also potential route for images

getRecipes({
	filters: RecipeQueryFilter[]
})//returns all public recipes that match filters

getUserRecipes({
	user: string,
	filters: RecipeQueryFilter[]
})//returns all user recipes that match filters

copyPublicRecipeToUser({

})//accepts recipe object id and user in req.params then copies the recipe to the user's private recipes

makeUserRecipePublic({

})//accepts a user and recipe title in req.body then creates a public recipe

rateRecipe({

})//accepts a user, rating, and recipe object id in req.body then adds to recipe rating and updates users ratings

createUser({

})//accepts a user email in req.body then creates user

createRecipe({

})//accepts a recipe object and user in req.body then adds the recipe to the user's document

updateRecipe({

})//accepts a user and recipe object in req.body then updates the recipe

deleteUserRecipe({

})//accepts a user and recipe title in req.params then deletes recipe from user's document
```

Example

```javascript
const recipes = getUserRecipes({
	user: currentUser,
	filters: [{type: 'ingredient', val: ['carrots', 'rice']},]
})


```

#### Database Schema

##### User Schema

```javascript
const userSchema = new mongoose.Schema({
	email: {type: String, required: true, unique: true},
	recipes: {type: [recipeSchema], required: false},
	ratings: {type: [ratingSchema], required: false}
	});
const recipeSchema = new mongoose.Schema({
	user: {type: String, required: false}
	title: {type: String, required: true},
	ingredients: {type: [String], required: true},
	tags: {type: [String], required: false},
	time: {type: number, require: false},
	rating: {type: Number, reqired: false},
	totalRatings: {type: Number, required: false},
	steps: {type: stepSchema, required: true}
	});
const ratingSchema = new mongoose.Schema({
	recipes: {type: [Schema.Types.ObjectId], ref: 'Recipe'},
	ratings: {type: Number, required: true}
	});
const stepSchema = new mongoose.Schema({
	orderd: {type: Number, required: true}
	instructions: {type: String, required: false},
	file: {type: String, required: false},
	time: {type: Number, required: false}
	});
```
