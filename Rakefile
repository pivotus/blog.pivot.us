# == Dependencies ==============================================================

require 'rake'
require 'fileutils'

# Set "rake watch" as default task
task :default => :watch

# Get and parse the date
DATE = Time.now.strftime("%Y-%m-%d")
TIME = Time.now.strftime("%H:%M:%S")

# == Helpers ===================================================================

# Execute a system command
def execute(command)
  system "#{command}"
end

# Chech the title
def check_title(title)
  if title.nil? or title.empty?
    raise "Please add a title to your file."
  end
end

# Transform the filename and date to a slug
def transform_to_slug(title)
  characters = /("|'|!|\?|:|\s\z)/
  whitespace = /\s/
  turkish_characters = {'Ş' => 's', 'ş' => 's', 'Ö' => 'o', 'ö' => 'o', 'İ' => 'i' , 'ı' => 'i', 'Ü' => 'u', 'ü' => 'u', 'Ğ' => 'g', 'ğ' => 'g', 'Ç' => 'c', 'ç' => 'c'}
  transformed_title = title.dup
  turkish_characters.each {|k,v| transformed_title.gsub!(k,v)}
  "#{transformed_title.gsub(characters,"").gsub(whitespace,"-").downcase}.md"
end

# Read the template file
def read_file(template)
  File.read(template)
end

# Save the file with the title in the YAML front matter
def write_file(content, title, category, filename)
  parsed_content = "#{content.sub("title:", "title: \"#{title}\"")}"
  parsed_content = "#{parsed_content.sub("categories:", "categories: #{category}")}"
  parsed_content = "#{parsed_content.sub("author:", "author: #{ENV['USER']}")}"
  File.write("_posts/#{category}/#{filename}", parsed_content)
  puts "#{filename} was created in '_posts/#{category}'."
end

# Create the file with the slug and open the default editor
def create_file(category, filename, content, title)
  raise "_posts/#{category} not exists" unless File.exists?("_posts/#{category}")
  if File.exists?("_posts/#{category}/#{filename}")
    raise "The file already exists."
  else
    write_file(content, title, category, filename)
    editor = ENV['EDITOR']
    if editor && !editor.nil?
      sleep 1
      execute("#{editor} _posts/#{category}/#{filename}")
    end
  end
end

# Get the "open" command
def open_command
  if RbConfig::CONFIG["host_os"] =~ /mswin|mingw/
    "start"
  elsif RbConfig::CONFIG["host_os"] =~ /darwin/
    "open"
  else
    "xdg-open"
  end
end

# == Tasks =====================================================================

# rake post["category", "Title"]
# rake post["articles", "Article Title Here"]
# rake post["blog", "Blog Title Here"]
desc "Create a post in _posts"
task :post, :category, :title do |t, args|
  category = args[:category]
  title = args[:title]
  template = "_templates/post"
  check_title(title)
  filename = "#{DATE}-#{transform_to_slug(title)}"
  content = read_file(template)
  create_file(category, filename, content, title)
end

# rake build
desc "Build the site"
task :build do
  execute("jekyll build")
end

# rake watch
desc "Serve and watch the site"
task :watch do
  execute("jekyll serve --watch")
end

# rake preview
desc "Launch a preview of the site in the browser"
task :preview do
  Thread.new do
    puts "Launching browser for preview..."
    sleep 1
    execute("#{open_command} http://localhost:4000/")
  end
  Rake::Task[:watch].invoke
end

# rake deploy["Commit message"]
desc "Deploy the site to a remote git repo"
task :deploy, :message do |t, args|
  message = args[:message]
  branch = "gh-pages"
  if message.nil? or message.empty?
    raise "Please add a commit message."
  end
  if branch.nil? or branch.empty?
    raise "Please add a branch."
  else
    Rake::Task[:build].invoke
    execute("git add .")
    execute("git commit -m \"#{message}\"")
    execute("git push origin #{branch}")
  end
end
