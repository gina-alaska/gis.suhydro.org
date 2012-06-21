desc "Add new dataset"
task :dataset do
  abort('rake aborted: _posts directory not found.') unless FileTest.directory?('_posts')

  title = ENV['title'] || 'new-post'

  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')

  begin
    date = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d')
  rescue Exception => e
    puts "Error - date format must be YYYY-MM-DD, please check you typed it correctly!"
    exit-1
  end

  filename = File.join('_posts', "#{date}-#{slug}.md")
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
end

desc "Compile the site"
task :compile do
  system('jekyll /www/hydro/htdocs')
end
