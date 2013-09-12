
task :default do
  puts "you don't know what you want to do.  use rake -T"
end

desc "Add new dataset"
task :dataset do
  require 'highline/import'

  abort('rake aborted: _posts directory not found.') unless FileTest.directory?('_posts')

  title = ENV['title'] || 'new-post'

  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')

  filename = File.join('data', "#{slug}.textile")
  if File.exists?(filename)
    abort('rake aborted!') if ask("#{filename} already exists.  Do you want to overwrite?", ['y','n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: default"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "---"
    post.puts "content goes here"
  end

  puts "Please add: data/#{slug}.html to _layouts/default.html"
end

desc "Start local server"
task :server do
  puts "Starting server on port 5000!"
  system "jekyll serve -P 5000 -w"
end

desc "Compile the site"
namespace :compile do
task :production do
  system('jekyll build -d /www/gis.suhydro.org/htdocs')
#  system('cp data/2012-rapid_eye/.htaccess /www/hydro/htdocs/data/2012-rapid_eye/.htaccess')
end
end
