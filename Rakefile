desc 'Recreates .box file'
task :rebuild do
  unless Dir.exists?('./modules')
    sh 'librarian-puppet install'
  end
  sh "vagrant destroy -f"
  sh 'vagrant up'
  sh 'vagrant ssh -c "sudo apt-get update && sudo apt-get upgrade -y"'
  sh 'vagrant reload' # To ensure the VM can boot properly after the upgrade

  # FROM: https://gist.github.com/3775253
  sh 'vagrant ssh -c "sudo /vagrant/purge.sh"'

  require 'time'
  box_file_name = "quantal64-rails-#{Date.today}.box"
  sh "rm -f #{box_file_name} && vagrant package --output #{box_file_name}"
end