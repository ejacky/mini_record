require "bundler/gem_tasks"
require "rake"
require "rake/testtask"

%w(install release).each do |task|
  Rake::Task[task].enhance do
    sh "rm -rf pkg"
  end
end

desc "Bump version on github"
task :bump do
  if `git status -s`.strip == ""
    puts "\e[31mNothing to commit (working directory clean)\e[0m"
  else
    version  = Bundler.load_gemspec(Dir[File.expand_path('../*.gemspec', __FILE__)].first).version
    sh "git add .; git commit -a -m \"Bump to version #{version}\""
  end
end

task :release => :bump
Rake::TestTask.new(:test) do |test|
  test.libs << 'spec'
  test.test_files = Dir['spec/**/*_spec.rb']
  test.verbose = true
end

task :default => :test
task :spec    => :test
