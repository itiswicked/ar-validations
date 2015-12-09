* Validate that the title of each recipe exists.
```ruby
validates :title, presence: true

r = Recipe.new(body: "A recipe")
r.save
r.errors
#=> {:name=>["can't be blank"]}

```

* Validate that the title of each recipe is unique.
* Add a field `servings` to your Recipe table. This field is optional, but if supplied, it must be greater than or equal to 1. Write a validation for this.
```ruby
validates :title, uniqueness: true
validates :servings, numericality: { greater_than_or_equal_to: 1 }, allow_blank: true

r = Recipe.new(
  name: "Brussels sprouts",
  body: "A great dish often never thought about.",
  servings: 0
)
r.save
r.errors
#=> {:name=>["has already been taken"], :servings=>["must be greater than 1"]}
```

* Validate that the title of each recipe contains "Brussels sprouts" in it.
```ruby
validates :name, format: { with: /Brussels sprouts/, message: "wrong format" }

r = Recipe.new(name: "Revenge", body: "Best served cold")
r.save
r.errors
#=> {:name=>["wrong format"]}
```

* Validate that the length of a comment be a maximum of 140 characters long.
```ruby
validates :body, length: { maximum: 140 }

c = Comment.new(recipe_id: 1, body: "A really long comment that hopefully will break the application. A fool and his head are soon parted. Qapla! Need just a few more characters.... good.")
c.save
c.errors
#=> {:body=>["is too long (maximum is 140 characters)"]}
```

* Validate that a comment has a recipe.
```ruby
validates_associated :recipe

c = Comment.new(recipe_id: 1000, body: "Breaka da app, droppa da base.")
c.save
c.errors
#=> {:recipe=>["can't be blank"]}
```


``
