require 'pry'
require 'rake/clean'

source_files = Rake::FileList["*.md"]

def cleaverized_name(source)
  source.gsub(/\.md\z/, '-cleaver.html')
end

CLEAN.include(source_files.map(&method(:cleaverized_name)))
CLEAN.include(source_files.ext('html'))

task default: :html

task :html => source_files.ext('html')

rule '.html' => '.md' do |t|
  sh "cleaver #{t.source}"
  FileUtils.mv(cleaverized_name(t.source), t.name)
end
