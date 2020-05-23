## What's this about?
It's a rails app demo to showcase how to use devise with another authentication key that's not email.

## [Inspiration](https://github.com/heartcombo/devise/wiki/How-To:-Allow-users-to-sign-in-with-something-other-than-their-email-address)

## How to
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

4. Add changes to the views
```erb
  <div class="field">
    <%= f.label :username %><br />
    <%= f.email_field :username, autofocus: true, autocomplete: "username" %>
  </div>
```


5. Config locales (if need be)

Change from
```yml
invalid: 'Invalid email or password.'
not_found_in_database: 'Invalid email or password.'
```
To
```yml
invalid: 'Invalid username or password.'
not_found_in_database: 'Invalid username or password.'
```