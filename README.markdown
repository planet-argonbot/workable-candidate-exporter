# Workable Exporter

This rake task will connect to the Workable API and create an export of every
candidate who applied for a Ruby on Rails related position.

It skips any candidates we disqualified and/or hired.

## Setup local environment to run

1. Create a .env file and add something like this:

```bash
  % touch .env

# Then add the following bit with your API key to the .env file

# .env
# Workable API settings
API_KEY=3333REPLACE-WITH-YOUR-API-KEY333
SUBDOMAIN=planetargon
```

Note:  You can find your API KEY at:

* https://planetargon.workable.com/backend/settings/integrations

2. Install Ruby version

```bash
  % rbenv install
```

3. Install bundler

```bash
  % gem install bundler
```

4. Install your gems

```bash
  % bundle install
```


5. Run the task

```bash
  bundle exec rake
```

6. You can find the CSV files in the `export/` directory.

FIN.
