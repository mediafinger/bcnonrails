require 'capistrano_colors'
require 'bundler/capistrano'
require 'provizioning/puppet'

load 'deploy' if respond_to?(:namespace) # cap2 differentiator
Dir['vendor/plugins/*/recipes/*.rb'].each { |plugin| load(plugin) }
load 'config/deploy'

namespace :deploy do
  task :symlink_config_files do
    ["config/database.yml"].each do |file|
      run "rm -f #{deploy_to}/current/#{file}"
      run "ln -s #{deploy_to}/shared/files/#{file} #{deploy_to}/current/#{file}"
    end
  end
end

after "deploy:create_symlink", "deploy:symlink_config_files"