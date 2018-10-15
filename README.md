### NoBrainer
---
https://github.com/nviennot/nobrainer

http://nobrainer.io/

```
gem 'nobrainer'

```

```ruby
class User
  include NoBrainer::Document
  field :name
  field :email
end

User.create(:name => 'Nico', :email => 'nicolas@viennot.biz')
User.count

```

```
class User
  include NoBrainer::Document
end

class Admin < User
end

class User
  include NoBrainer::Document
  filed :first_name
  filed :last_name
end

class User
  include NoBrainer::Document
  filed :email
  def email=(value)
    super(value.strip.downcase)
  end
end

filed :num_friends, :default => 0
filed :create_at, :default => -> [ Time.now ]

filed :email, :type => String
field :email, :validates => [ :format => [ :with => /@/ ] ]
filed :email, :index => true
filed :email, :store_as => :e

class User
  field :email, :type => String
  filed :avatar, :type => Binary, :lazy_fetch => true
end
user = User.first
user.email
user.avatar

class User
  virtual_field :current_user_following do |doc|
    if Thread.current[:current_user]
      Followship.where(:follower_id => doc[:id], :following_id =>
Thread.current[:current_user].id).to_rql.is_empty.not
    end
  end
end



```

