require "rubygems"
require 'rake'
require 'yaml'
require 'time'

SOURCE = "."
CONFIG = {
  'version' => "12.3.2",
  'themes' => File.join(SOURCE, "_includes", "themes"),
  'layouts' => File.join(SOURCE, "_layouts"),
  'posts' => File.join(SOURCE, "_posts"),
  'post_ext' => "md",
  'theme_package_version' => "0.1.0"
}

# Usage: rake post title='A Title'
desc "Begin a new post in #{CONFIG['posts']}"
task :post do
  abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])

  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  begin
    date = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d')
  rescue Exception => e
    puts "Error - date format must be YYYY-MM-DD, please check you typed it correctly!"
    exit -1
  end
  filename = File.join(CONFIG['posts'], "#{date}-#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "date: #{date}"
    post.puts "author: Leo"
    post.puts "permalink: /#{slug}-#{Time.now.strftime('%Y%m%d')}/"
    post.puts ""
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: \"\""    
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post

desc "Launch dev environment"
task :dev do
  system "bundle exec jekyll serve --livereload"
end # task :dev

desc "Launch project build"
task :build do
  system "bundle exec jekyll build"
end # task :build

#Load custom rake scripts
Dir['_rake/*.rake'].each { |r| load r }
