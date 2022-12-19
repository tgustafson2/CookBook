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
getRecentRecipes()

getRecipes({
	filters: RecipeQueryFilter[]
})

getUserRecipes({
	user: string,
	filters: RecipeQueryFilter[]
})
```

Example

```javascript
const recipes = getUserRecipes({
	user: currentUser,
	filters: [{type: 'ingredient', val: ['carrots', 'rice']},]
})


```
