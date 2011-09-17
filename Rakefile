require 'open-uri'
require 'airbrake'

class Heartbeat
  PULSE_RATE = ENV['PULSE_RATE'].to_i || 60

  def self.pulse
    begin
      open ENV['URI']
    rescue Exception => exception
      Airbrake.notify(
        :error_class => "Site Unreachable",
        :error_message => "Site Unreachable: #{exception.message}",
        :parameters => { :action => ENV['URI'] }
      )
    ensure
      sleep(PULSE_RATE)
      pulse
    end
  end
end

Airbrake.configure do |config|
  config.api_key = ENV['AIRBRAKE_API_KEY']
  config.rescue_rake_exceptions = true
end

task :heartbeat do
  Heartbeat.pulse
end
