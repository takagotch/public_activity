### public_activity
---

https://github.com/chaps-io/public_activity

```sh
gem install public_activity
gem 'public_activity'

rails g public_activity:migration
rake db:migrate

```


```ruby
# config/initializers/public_activity.rb
PublicActivity::Config.set do
  orm :mongoid
end

# config/initializers/public_activity.rb
PublicActivity::Config.set do
  org :mongo_mapper
end

class Article < ActiveRecord::Base
  include PublicActivity::Model
  tracked
end

class Article
  include Mongoid::Document
  include PublicActivity::Model
  tracked
end

class Article
  include MongoMapper::Document
  include PublicActivity::Model
  tracked
end


@article.create_activity key: 'article.commented_on', owner: current_user

# notifications_controller.rb
def index
  @activities = PublicActivity::Activity.all
end

<%= render_activities(@activities) %>
<%= render_activities(@activities, layout: :activity) %>
<%= render_activity(@activity, locals: {friends: current_user.friends}) %>

# app/views/public_activity/user/_changed_avatar.(erb|haml|slim)

# rails_helper.rb
require 'public_activity/testing'
PublicActivity.enabled = false

# file_spec.rb
PulicActivity.with_tracking do
end

PublicActivity.without_traking do
end
```

```.yml
activity:
  article:
    create: 'Article has been created'
    update: 'Someone has edited the article'
    destroy: 'Some user removed an article!'
```
https://github.com/chaps-io/public_activity/wiki/%5BHow-to%5D-Set-the-Activity's-owner-to-current_user-by-default
