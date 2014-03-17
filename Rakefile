require "bundler"
require "rake"
require "bundler/gem_tasks"
require "rspec/core/rake_task"
$:.unshift File.join(File.dirname(__FILE__), *%w[.. lib])

require 'pry'
require "quandl/client"

include Quandl::Client

config = OpenStruct.new(YAML.load(File.read("#{ENV['HOME']}/.quandl/config")))

Quandl::Client.use config.quandl_url
Quandl::Client.token = config.token

task :default => :spec

desc "Run all specs"
RSpec::Core::RakeTask.new(:spec) do |task|
  task.pattern = "spec/**/*_spec.rb"
end

task :console do |t, args|
  binding.pry
end

require 'quandl/utility/rake_tasks'
Quandl::Utility::Tasks.configure do |c|
  c.name              = 'quandl_client'
  c.version_path      = 'VERSION'
  c.changelog_path    = 'UPGRADE.md'
  c.changelog_matching  = ['^QUGC','^WIKI']
end
