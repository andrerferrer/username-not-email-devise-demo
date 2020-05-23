
[Inspiration](https://github.com/heartcombo/devise/wiki/How-To:-Allow-users-to-sign-in-with-something-other-than-their-email-address)

1. Add the config to config/initializers/devise.rb

```ruby
  # Login with username
  config.authentication_keys = [:username]
```

2. create a migration and run it
```ruby
	rails generate migration AddUsernameToUsers username:string:uniq
```

3. Add validation to the User model

```ruby
# Add validation
  validates :username, uniqueness: true
```

