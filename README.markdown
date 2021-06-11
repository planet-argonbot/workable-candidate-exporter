# Workable Candidate Exporter

This rake task will connect to the Workable API and create an export of every
candidate who applied for a Ruby on Rails related position.

It skips any candidates we disqualified and/or hired.

## Setup environment to run

1. Create a .env file and add something like this:

```bash
  % touch .env

```
2. Add the following bit with your API key to the .env file

```ruby
# .env
# Workable API settings
API_KEY=3333REPLACE-WITH-YOUR-API-KEY333
SUBDOMAIN=planetargon
```

Note:  You can find your API KEY at:

* https://planetargon.workable.com/backend/settings/integrations

3. Install Ruby and bundler

```bash
  % rbenv install && gem install bundler
```

4. Install your gems

```bash
  % bundle install
```


5. Run the Rake task

```bash
  % bundle exec rake
```

6. Voila, you can find the CSV files in the `export/` directory.

FIN.


## License

Workable Candidate Exporter is released under the [MIT license](LICENSE).

## About Planet Argon

![Planet Argon](https://pa-github-assets.s3.amazonaws.com/PARGON_logo_digital_COL-small.jpg)

Created by the team at [Planet Argon](https://www.planetargon.com/?utm_source=github), a [Ruby on Rails development agency](https://www.planetargon.com/skills/ruby-on-rails-development?utm_source=github). Check out our [other open source projects](https://www.planetargon.com/open-source?utm_source=github).
