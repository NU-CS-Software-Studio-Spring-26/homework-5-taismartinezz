##Stack

This project uses Rails 8.1.3 with Ruby 3.4.1 and SQLite3.
The frontend uses ERB templates, Hotwire (Turbo + Stimulus), Propshaft, and Importmap instead of Node.
Jbuilder is used for JSON responses.
Testing is done with Minitest, Capybara, and Selenium for system tests.
Background jobs use Active Job with SolidQueue in production.

##Commands
Setup project: bin/setup
Run app: bin/dev
Run tests: bin/rails test
Run system tests: bin/rails test:system
Run linter: bin/rubocop
Run security check: bin/brakeman --no-pager

##Conventions
Controllers should respond with HTML and Turbo Streams, not custom JavaScript
Shared partials go in app/views/shared/
Authorization logic should stay in controllers or services, not views
Use Rails generators for migrations and models instead of writing them manually
Every controller must use strong parameters

##Don'ts
Don’t add new gems without approval
Don’t use inline JavaScript inside ERB files
Don’t disable CSRF protection with skip_before_action :verify_authenticity_token
Don’t use real user data in seeds
Don’t copy models or migrations from other projects