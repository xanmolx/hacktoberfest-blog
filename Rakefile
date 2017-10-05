
require 'fileutils'

#rake post:new to create a new post

namespace :post do
  desc "Creating a new post"
  task :new do
    #set today's date
    get_date = Time.now.to_s
    split_date = get_date.split(" ")
    @date = split_date[0]
    #get title
    puts "What's the name for your post?"
    @name = STDIN.gets.chomp
    @slug = "#{@name}"
    @slug = @slug.tr('ÁáÉéÍíÓóÚú', 'AaEeIiOoUu')
    @slug = @slug.downcase.strip.gsub(' ', '-')
    #get category
    puts "What is your name?"
    @author = STDIN.gets.chomp
    FileUtils.touch("_posts/#{@date}-#{@slug}.markdown")
    open("_posts/#{@date}-#{@slug}.markdown", 'a' ) do |file|
      file.puts "---"
      file.puts "layout: 'post'"
      file.puts "title: '#{@name}'"
      file.puts "date: #{@date}"
      file.puts "author: '#{@author}'"
      file.puts "excerpt: 'QUICK BLURB OF YOUR POST HERE'"
      file.puts "twitter: 'LEAVE BLANK IF NO TWITTER'"
      file.puts "github: 'LEAVE BLANK IF NO GITHUB'"
      file.puts "website: 'LEAVE BLANK IF NO WEBSITE'"
      file.puts "---"
    end
  end
end