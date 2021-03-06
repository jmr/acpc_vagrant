# acpc_vagrant
Vagrant virtual machine set up for developing, testing, and (possibly) deploying the ACPC poker GUI client and related gems.

## Developing with forks of the original ACPC repositories
Edit the paths in `grab_projects.sh` to retrieve your fork of the ACPC repositories if desired.

## Zero to Playing Poker

0. Download this repository
1. Install Ruby (>= 1.9.2)
    - On Windows, go to <http://rubyinstaller.org/downloads/> and install:
        1. Ruby 2.1.6
            - Ensure that the "Add Ruby executables to your PATH" is selected during installation so you can run the `gem` and `bundle` later.
        2. The corresponding DevKit
            - Follow these [Quick Start](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit#quick-start) instructions.
2. Install Bundler, `gem install bundler`
3. Install gems, `bundle install` in project root)
4. Install cookbooks, `librarian-chef install`
5. Start the virtual machine, `vagrant up`
    - This step could take tens of minutes
    - If connecting to the VM times out, but you can still manually connect to it afterwards, then run `vagrant halt` and `vagrant up` or `vagrant reload`. This occurred for me on Windows and vagrant was able to complete the VM setup after restarting.
6. Log in to the virtual machine, `vagrant ssh` on Linux or OSX, [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) on Windows
    - On Windows, you can try `vagrant ssh` first, but if that fails, follow [these instructions](https://github.com/Varying-Vagrant-Vagrants/VVV/wiki/Connect-to-Your-Vagrant-Virtual-Machine-with-PuTTY). Afterwards, you should be apply to access the VM from PuTTY or `vagrant ssh`.
7. Navigate to shared project directory, `cd /vagrant/repositories/acpc_poker_gui_client`
8. Install gems, `bundle install`
9. Compile the ACPC server project, `bundle exec acpc_dealer compile`
10. Start background worker, `bundle exec sidekiq -r ./ -L ./log/sidekiq.log -t 1 &`
11. Start the Rails server, `bundle exec rails s`
12. Point your browser to `localhost:3000`, and you should see the match start screen. You should now be able to start a match. If that succeeds, congratulations, you've completed the set up!
