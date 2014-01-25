# https://github.com/plusjade/jekyll-bootstrap/blob/master/Rakefile
# Usage: rake post title="A Title" [date="2012-02-09"] [tags=[tag1,tag2]] [category="category"]
desc "Begin a new post in _posts}"
task :post do
  abort("rake aborted: '_posts' directory not found.") unless FileTest.directory?('_posts')
  title = ENV["title"] || "new-post"
  tags = ENV["tags"] || "[\"#000000\"]"
  category = ENV["category"] || ""
  category = "\"#{category.gsub(/-/,' ')}\"" if !category.empty?
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  begin
    date = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d')
  rescue => e
    puts "Error - date format must be YYYY-MM-DD, please check you typed it correctly!"
    exit -1
  end
  filename = File.join('_posts', "#{date}-#{slug}.md")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: default"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "tags: #{tags}"
    post.puts "---\n\n"
    post.puts "[![#{title.gsub(/-/,' ')}](/images/#{slug}.jpg \"Words\")](/images/#{slug}.jpg)"
  end
end # task :post


def ask(message, valid_options)
  if valid_options
    answer = get_stdin("#{message} #{valid_options.to_s.gsub(/"/, '').gsub(/, /,'/')} ") while !valid_options.include?(answer)
  else
    answer = get_stdin(message)
  end
  answer
end

def get_stdin(message)
  print message
  STDIN.gets.chomp
end

task :default => 'post'
