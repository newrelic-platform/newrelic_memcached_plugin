## Memcached Ruby Plugin for New Relic

Prerequisites
-------------
- A New Relic account. Signup for a free account at [http://newrelic.com](http://newrelic.com)
- A server running Memcached v1.4 or greater. Download the latest version of Memcached for free [here](https://code.google.com/p/memcached/downloads/list).
- Ruby version 1.8.7 or better

Running the Agent
----------------------------------

1. Download the latest `newrelic_memcached_plugin-X.Y.Z.tar.gz` from [the tags list](https://github.com/newrelic-platform/newrelic_memcached_plugin/tags)
1. Extract the downloaded archive to the location you want to run the Memcached agent from
1. Run `bundle install` to install required gems
1. Copy `config/template_newrelic_plugin.yml` to `config/newrelic_plugin.yml`
1. Edit `config/newrelic_plugin.yml` with your license key and to point to your instances of Memcached. You can add as many hosts as you'd like If your Memcached instances are bound to an external IP, use that value for the host field.  If you omit the 'port' field it will default to '11211'
1. Edit the `config/newrelic_plugin.yml` file by changing the name and endpoint fields to match your Memcached server configuration
1. From your shell run: `./newrelic_memcached_agent`
1. Wait a few minutes for New Relic to begin processing the data sent from your agent.
1. Log into your New Relic account at [http://newrelic.com](http://newrelic.com) and click on `Memcached` on the left hand nav bar to start seeing your Memcached metrics

Using Monit to keep the Agent running
-------------------------------------

On Ubuntu: `sudo apt-get install monit`

Example config file:

```
check process newrelic_memcached_agent
  with pidfile /home/ubuntu/newrelic_memacached_agent/newrelic_memcached_agent.pid
  start program = "/bin/su - ubuntu -c '/home/ubuntu/newrelic_memcached_agent/newrelic_memcached_agent.daemon start'" with timeout 90 seconds
  stop program = "/bin/su - ubuntu -c '/home/ubuntu/newrelic_memcached_agent/newrelic_memcached_agent.daemon stop'" with timeout 90 seconds
  if totalmem is greater than 250 MB for 2 cycles then restart
  group newrelic_agent
```

Source Code
-----------

This plugin can be found at [https://github.com/newrelic-platform/newrelic_memcached_plugin](https://github.com/newrelic-platform/newrelic_memcached_plugin)
