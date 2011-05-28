# Hey, Emacs!  This file contains -*- ruby -*- stuff.

task :default => 'deploy:joyent'

namespace :deploy do
  desc "Run the update script unless Windows"
  task :mydomain do |t|
    if RUBY_PLATFORM =~ /darwin/ && File.exist?('update')
      puts "old bash script"
      system './update'
    else
      puts "no.  I just won't do anything."
    end
  end

  desc "Run the update.joy script unless Windows"
  task :joyent do |t|
    if File.exist?(xferlist = File.expand_path('~/code/ruby/xferlist.rb'))
      #puts "ruby script"
      system "#{xferlist} lovelandcanoe@richardson.joyent.us:domains/kayakcincinnati.com web cgi-bin"
    elsif RUBY_PLATFORM =~ /darwin/ && File.exist?('update.joy')
      puts "bash script"
      system './update.joy'
    else
      puts "no.  I just won't do anything."
    end
  end
end
# the remainder is unused for LovelandCanoe.com

desc "Fail unless svn status of ./src is clean"
task :cleansvn do |t|
  src = 'src'
  svnstat = 'svn status --show-updates'
  svnout = Dir.chdir(src) { |d| `#{svnstat}` }
  if (lines = svnout.split($/).size) > 1
    puts "The svn status on the #{src} directory wasn't empty (#{lines} line#{'s' unless lines == 1})."
    puts "Do you need to commit something? "
    puts "> #{svnstat}\n#{svnout}"
    raise "NotSvnClean"
  end
end

desc "Pull updates from repository"
task :update => [ :update_src, :update_tools ]

task :update_src do
  src = 'src'
  puts "Update '#{src}'..."
  Dir.chdir(src) { |d| system "svn update" }
  puts "done."
end

task :update_tools do
  puts "Update tools..."
  system "svn update"
  puts "done."
end

desc "Create the directory structure needed for webgen"
task :setup => 'README.html' do |t|
  directory "plugin"
  directory "public"
  directory "tmp/cache"
  directory "log"
end

file 'README.html' => [ 'README' ] do |t|
  sh "redcloth #{t.prerequisites.join(' ')} > #{t.name}"
end
