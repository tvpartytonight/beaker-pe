source ENV['GEM_SOURCE'] || "https://rubygems.org"

gemspec



def location_for(place, fake_version = nil)
  if place =~ /^(git:[^#]*)#(.*)/
    [fake_version, { :git => $1, :branch => $2, :require => false }].compact
  elsif place =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false }]
  else
    [place, { :require => false }]
  end
end


# We don't put beaker in as a test dependency because we
# don't want to create a transitive dependency
group :acceptance_testing do
  gem "beaker", *location_for(ENV['BEAKER_VERSION'] || '~> 3.0')
end

if ENV['GEM_SOURCE'] =~ /rubygems\.delivery\.puppetlabs\.net/
  gem "scooter", *location_for(ENV['SCOOTER_VERSION'] || '~> 2.0')
end


if File.exists? "#{__FILE__}.local"
  eval(File.read("#{__FILE__}.local"), binding)
end
