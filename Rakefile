namespace :book do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'images' unless Dir.exists? 'images'
    Dir.glob("book/*/images/*").each do |image|
      FileUtils.copy(image, "book/images/" + File.basename(image))
    end
  end

  desc 'build basic book formats'
  task :build => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor book/wap2013.asc -r asciidoctor-diagram`
    puts " -- HTML output at wap2013.html"

    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 book/wap2013.asc -r asciidoctor-diagram`
    puts " -- Epub output at wap2013.epub"

    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 book/wap2013.asc -r asciidoctor-diagram`
    puts " -- Mobi output at wap2013.mobi"

    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf book/wap2013.asc -r asciidoctor-diagram 2>/dev/null`
    puts " -- PDF  output at wap2013.pdf"
  end
end

task :default => "book:build"
