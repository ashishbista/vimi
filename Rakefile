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
	unless File.exist?("vim-haml")
		`git clone git://github.com/tpope/vim-haml.git`
	end
	Dir.mkdir(File.expand_path("~/.vim")) unless File.exist?(File.expand_path("~/.vim"))
	`cp -r vim-haml/* ~/.vim`
	`cd ~/.vim`

	# Install Rails plugin
	 unless File.exist?("vim-rails")
		`git clone git://github.com/tpope/vim-rails.git`
		 `cp -r vim-rails/* ~/.vim`
	 end
	 unless File.exist?("vim-bundler")
		`git clone git://github.com/tpope/vim-bundler.git`
	end
end
