## What's this about?
It's a rails app demo to showcase how to use devise with another authentication key that's not email.
We're going to keep email on the User, though.

## [Inspiration](https://github.com/heartcombo/devise/wiki/How-To:-Allow-users-to-sign-in-with-something-other-than-their-email-address)

## How to
1. Add the config to config/initializers/devise.rb

```ruby
  # Login with username
  config.authentication_keys = [:username]
```

2. Create a migration and run it
```ruby
	rails generate migration AddUsernameToUsers username:string:uniq
```

3. Add validation to the User model

```ruby
# Add validation
  validates :username, uniqueness: true, presence :true
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

6. Config Devise to keep accepting email when creating
```ruby
  before_action :configure_permitted_parameters, if: :devise_controller?

  def configure_permitted_parameters
    # For additional fields in app/views/devise/registrations/new.html.erb
    devise_parameter_sanitizer.permit(:sign_up, keys: [:email])

    # For additional in app/views/devise/registrations/edit.html.erb
    # devise_parameter_sanitizer.permit(:account_update, keys: [:email])
  end
```