require 'fileutils'
task :default => [:setup]

task :setup do
	 %w[ vimrc ].each do |file|
		 dest = File.expand_path(("~/.#{file}"))
		 unless File.exist?(dest)
			 ln_s(File.expand_path("#{file}", __FILE__), dest)
		 end
	 end

	# Haml support
	unless File.exists?("vim-haml")
		`git clone git://github.com/tpope/vim-haml.git`
	end
	Dir.mkdir(File.expand_path("~/.vim")) unless File.exists?(File.expand_path("~/.vim"))
	`cp -r vim-haml/* ~/.vim`
	`cd ~/.vim`

	# Install Rails plugin
	`wget -c http://www.vim.org/scripts/download_script.php?src_id=16429 -o rails-vim.zip`
	`unzip rails-vim.zip ~/.vim`
end
