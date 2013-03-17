require 'fileutils'
task :default => [:setup]

task :setup do
  # Create unified swap directory
  Dir.mkdir(File.expand_path("~/.vim/swaps")) unless File.exist?(File.expand_path("~/.vim/swaps"))

  # Copy rc files
  %w[ vimrc ].each do |file|
     dest = File.expand_path(("~/.#{file}"))
     cp file, dest
   end

  Dir.mkdir(File.expand_path("~/.vim")) unless File.exist?(File.expand_path("~/.vim"))

  plugins = {
    'vim-haml' => 'git://github.com/tpope/vim-haml.git',
    'vim-rails' => ' git://github.com/tpope/vim-rails.git',
    'vim-bundler' => 'git://github.com/tpope/vim-bundler.git',
    'ack.vim' => 'git://github.com/mileszs/ack.vim.git'
  }

  plugins.each do |k, v|
    unless File.exist?(k)
      sh "git clone #{v}"
      sh "cp -r #{k}/* ~/.vim"
    end
  end
  puts "Setup completed. Enjoy!"
end

task :update do
  desc "Updates the library"
  sh "git pull"
  Rake::Task['setup'].invoke
end
