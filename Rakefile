require 'rubygems'
gem 'hoe', '>= 2.1.0'
require 'hoe'
require 'fileutils'
require './lib/despamilator'

Hoe.plugin :newgem
# Hoe.plugin :website
# Hoe.plugin :cucumberfeatures

# Generate all the Rake tasks
# Run 'rake -T' to see list of generated tasks (from gem root directory)
$hoe = Hoe.spec 'despamilator' do
  self.developer 'Stephen Hardisty', 'moowahaha@hotmail.com'
  self.post_install_message = 'PostInstall.txt'
  self.rubyforge_name       = self.name # TODO this is default value
  # self.extra_deps         = [['activesupport','>= 2.0.2']]

end

require 'newgem/tasks'
Dir['tasks/**/*.rake'].each { |t| load t }

# TODO - want other tests/tasks run by default? Add them to the list
# remove_task :default
task :test => [:spec]
task :default => [:test]
task :install => [:install_gem]

desc 'Generate relevant documentation.'
task :rdoc do
    sh 'rdoc lib/despamilator.rb lib/despamilator/filter_base.rb'
end

task :cultivate do
  sh "touch Manifest.txt; rake check_manifest |grep -v \"(in \" | patch"
  sh "cat Manifest.txt  | grep -v 'bundle/config' | grep -v '_corpus' > Manifest.txt2"
  sh "mv Manifest.txt2 Manifest.txt"
  sh "rake debug_gem | grep -v \"(in \" > `basename \\`pwd\\``.gemspec"
end
