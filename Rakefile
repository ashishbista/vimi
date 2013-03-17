require 'fileutils'
task :default => [:setup]

task :setup do
  # Create unified swap directory
  Dir.mkdir(File.expand_path("~/.vim/swaps")) unless File.exist?(File.expand_path("~/.vim/swaps"))

  # Copy rc files
  %w[ vimrc ].each do |file|
     dest = File.expand_path(("~/.#{file}"))
     unless File.exist?(dest)
       ln_sf(File.expand_path("#{file}", __FILE__), dest)
     end
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

end
