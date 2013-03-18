require 'fileutils'
task :default => [:setup]

task :setup do
  # Create unified swap directory
  Dir.mkdir(File.expand_path("~/.vim")) unless File.exist?(File.expand_path("~/.vim"))
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
    'ack.vim' => 'git://github.com/mileszs/ack.vim.git',
    'vim-fugitive' => 'git://github.com/tpope/vim-fugitive.git',
    'ctrlp.vim' => 'git://github.com/kien/ctrlp.vim.git'
  }

  plugins.each do |k, v|
    unless File.exist?(k)
      sh "git clone #{v}"
      sh "cp -r #{k}/* ~/.vim"
    end
  end

  puts "Setup completed. Enjoy!"

end

task :configure do

  # The follwing steps are required for ctrl+s
  if ENV['SHELL'].include? "zsh"
    zsh_configs = <<-END
    alias vim="stty stop '' -ixoff ; vim"
    ttyctl -f
    END
    write_configs_to_file("~/.zshrc", zsh_configs)  
  elsif ENV['SHELL'].include? "bash"
    bash_configs = <<-END
    vim()
    {
      local STTYOPTS="$(stty --save)"
      stty stop '' -ixoff
      command vim "$@"
      stty "$STTYOPTS"
    }
    END
    write_configs_to_file("~/.bashrc", bash_configs)
  end
end

task :update do
  desc "Updates the library"
  sh "git pull"
  Rake::Task['setup'].invoke
end

def write_configs_to_file(file, configs)
   file = File.open(File.expand_path(file), "a")
   file.write configs
   file.close
end
