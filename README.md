# Acts As Commentable

Provides a single Comment model that can be attached to any model(s) within your app. It creates
a Comment model and handles the plumbing between that model and any models that you declare to be
commentable models.


## Installation :

Add the following line to your Gemfile

### Rails 4

```ruby
  gem 'acts_as_commentable'
```

## Generator

### Rails 3+

```cli
  rails g comment
```

Then migrate your database to add the comments model:

```cli
  rake db:migrate
```

## Usage

Make the desired ActiveRecord model act as commentable:

```ruby
  class Post < ActiveRecord::Base
    acts_as_commentable
  end
```

Add a comment to a model instance by adding the following to the controller:

```ruby
  commentable = Post.create
  comment = commentable.comments.create
  comment.title = "First comment."
  comment.comment = "This is the first comment."
  comment.save
```

Fetch comments for the commentable model by adding the following to the view:
 
```ruby
  commentable = Post.find(1)
  comments = commentable.comments.recent.limit(10).all
```

You can also add different types of comments to a model:

```ruby
  class Todo < ActiveRecord::Base
    acts_as_commentable :public, :private
  end
```

*Note:* This feature is only available from version 4.0 and above

To fetch the different types of comments for this model:

```ruby
  public_comments = Todo.find(1).public_comments
  private_comments = Todo.find(1).private_comments
```

By default, `acts_as_commentable` will assume you are using a `Comment` model.
To change this, or change any other join options, pass in an options hash:

```ruby
    class Todo < ActiveRecord::Base
      acts_as_commentable class_name: 'MyComment'
    end
```

This also works in conjunction with comment types:

```ruby
    class Todo < ActiveRecord::Base
      acts_as_commentable :public, :private, { class_name: 'MyComment' }
    end
```

## Credits

Xelipe - This plugin is heavily influenced by Acts As Taggable.

## Contributors

Jack Dempsey, Chris Eppstein, Jim Ray, Matthew Van Horn, Ole Riesenberg, ZhangJinzhu, maddox, monocle, mrzor, Michael Bensoussan, JP Ferreira

## More

http://www.juixe.com/techknow/index.php/2006/06/18/acts-as-commentable-plugin/
http://www.juixe.com/projects/acts_as_commentable
