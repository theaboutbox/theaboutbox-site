---
layout: post
title: "The Database is your Friend"
date: 2013-09-18 09:29
comments: true
categories: 
  - development
  - ruby
  - rails
---
Some lessons we are doomed to learn over and over again. In Rails,
ActiveRecord has a number of methods to help ensure the integrity of
your data, such as `validates_presence_of`, `validates_uniqueness_of`,
and `dependent: :destroy` on relations.

Those are useful for providing error messages when users submit forms,
but they are no guarantee that your data will stay consistent. In order
to do that, you need to define constraints on the database. Without
fail, every time I have ever forgotten to define not-null constraints,
unique indexes and foreign key relations, I have been bitten.

The issues can be very subtle, but here's an example

```ruby
def delete_removed_items(source_ids)
  Item.where.not(source_id: source_ids).delete_all
end
```

This code is part of a background process that synchronizes data with a
back-end service, and we are trying to delete items that no longer
exist. There is a problem, however. According to the Rails documentation
for [delete_all](http://apidock.com/rails/ActiveRecord/Relation/delete_all):

> Be careful with relations though, in particular :dependent rules 
> defined on associations are not honored. Returns the number of
> rows affected.

Oops! I guess the synchronization code doesn't delete any associations.
Now there are a bunch of orphaned records laying around. This is exactly
the kind of issue that would have been caught right away if the database
were enforcing a foreign key relation. Yeah, I picked the wrong method
in this case, but look, it gets worse. Here is what the Rails
documentation says for [validates_uniqueness_of](http://apidock.com/rails/ActiveRecord/Validations/ClassMethods/validates_uniqueness_of):

> Using this validation method in conjunction with ActiveRecord::Base#save 
> does not guarantee the absence of duplicate record insertions, because 
> uniqueness checks on the application level are inherently prone to race 
> conditions

So, lesson learned, again. By the way, the best way I know to make
foreign key relationships easy to deal with in Rails is to use the
excellent [Foreigner](https://github.com/matthuhiggins/foreigner)
plugin.
