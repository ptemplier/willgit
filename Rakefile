SCREENSHOTS = FileList["www/ss?.png"]

SCREENSHOTS_SMALL = SCREENSHOTS.map do |fn|
  fn =~ /ss(\d+)\.png/
  sfn = "www/ss#{$1}-small.png"
  file sfn => [fn] do |t|
    sh "cat #{fn} | pngtopnm | pnmscale -xysize 320 240 | pnmtopng > #{sfn}"
  end
  sfn
end

WWW_FILES = FileList["www/*"] - SCREENSHOTS - SCREENSHOTS_SMALL + FileList["bin/*"]

task :upload_webpage => WWW_FILES do |t|
  sh "scp -C #{t.prerequisites * ' '} wmorgan@rubyforge.org:/var/www/gforge-projects/git-wt-commit/"
end

task :upload_webpage_images => (SCREENSHOTS + SCREENSHOTS_SMALL) do |t|
  sh "scp -C #{t.prerequisites * ' '} wmorgan@rubyforge.org:/var/www/gforge-projects/git-wt-commit/"
end

# vim: syntax=ruby