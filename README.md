# Heartbeat

Stupid simple website uptime monitor. Run a `rake` task and get notified by
Airbrake if the site unreachable (essentially any response other than 2xx).

Usage:

    rake heartbeat URI=http://example.com AIRBRAKE_API_KEY=...

You can also set `PULSE_RATE=n` where `n` is the number of seconds to sleep
between pulses. The default is 60.

Designed to run as a worker on Heroku:

    git@github.com:grays/heartbeat.git
    cd heartbeat
    heroku apps:create my-heartbeat --stack cedar
    heroku config:add URI=http://example.com AIRBRAKE_API_KEY=...
    git push heroku master
    heroku scale worker=1
