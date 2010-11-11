require 'nanoc3/tasks'


desc "Generate a new blog post"
task :post do
  raise "Need to define a TITLE" if ENV['TITLE'].nil?
  title = ENV['TITLE']

  skeleton = <<-EOH
---
kind: article
title: #{ENV['TITLE']}
created_at: #{Time.now.strftime('%Y%m%dT%H%M%S')}
---
Put the content of the new blog post here
EOH
  filename = "#{title.gsub(/[,\. \-\'"\?]/,'_').downcase}.markdown"
  puts "filename: #{filename}"
  post_path = File.join './content/blog', filename
  
  File.open(post_path,'w') do |f|
    f.puts skeleton
  end

  if ENV['EDITOR']
    exec "#{ENV['EDITOR']} #{post_path}"
  end
end

namespace :deploy do
  desc "deploys the blog"
  task :github do
    exec 'git add . && git commit -m "New Blog Post" && git push origin master'
  end
end

task :deploy => ['deploy:github','deploy:rsync']
