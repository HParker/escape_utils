require 'bundler/gem_tasks'
require 'rake/testtask'
require 'ruby_memcheck'

RubyMemcheck.config(binary_name: "escape_utils/escape_utils")

test_config = lambda do |t|
  t.libs << "test"
  t.libs << "lib"
  t.test_files = FileList["test/**/*_test.rb"]
end

namespace :test do
  RubyMemcheck::TestTask.new(valgrind: :compile, &test_config)
end

Rake::TestTask.new do |t|
  t.libs << "test"
  t.libs << "lib"
  t.test_files = FileList["test/**/*_test.rb"]
end

task :default => :test

require "rake/extensiontask"

Rake::ExtensionTask.new('escape_utils') do |ext|
  ext.cross_compile = true
  ext.cross_platform = ['x86-mingw32', 'x86-mswin32-60']

  ext.lib_dir = File.join 'lib', 'escape_utils'
end

Rake::Task[:test].prerequisites << :compile


