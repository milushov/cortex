# TimeZones
## Person (User Model)
`validates_inclusion_of :time_zone, in: ActiveSupport::TimeZone.zones_map(&:name)`
## View Form
`:TODO Make ru_zones`
`form.time_zone_select :time_zone, ActiveSupport::TimeZone.us_zones`
## Controller 
` around_filter :person_time_zone, if: :current_person `
```
def person_time_zone(&block)
  Time.use_zone(current_person.time_zone, &block)
end
```
## Testing 
```
gem 'timecop'
gem 'zonebie'
```
## Using everytime
` Date.current ` isntead of ` Date.today `
` Time.zone.now ` instead of ` Time.now `

# RSS Feeds
Uses ActionView::Helpers::AtomFeedHelper
`index.atom.builder`
`content_for :head, auto_discovery_link_tag(:atom, some_url(form: 'atom'))`
We :can password protect rss feed

# Exception Notification
`gem 'exception_notification'` => `http://smartinez87.github.io/exception_notification/`
ignore default exceptions
`
App::Application.config.middleware.use ExceptionNotification::Rack,
  :ignore_exceptions => ExceptionNotifier.ignored_exceptions,
  :ignore_crawlers => %w{Googlebot bingbot},
 # :ignore_if => ->(env, exception) { exception.message =~ /^Couldn't find Page with ID=/ },
  :email => {
    :email_prefix => "[Whatever] ",
    :sender_address => %{"notifier" <notifier@example.com>},
    :exception_recipients => %w{exceptions@example.com}
  }
`
