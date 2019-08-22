# README
This document main purpose is to guide you through the necessary steps to create the docker environment for the application 

Ruby has many version compatibilities so normally is necessary to install a manager rvm if you want your ide to understand ruby

A Error should pop up during the installation and that's ok just follow the instructions and you will be fine  

- Error will be on docker-compose line 6 referring to mounted directory tmp the next step with chown fixes this  

https://www.howtoforge.com/tutorial/ubuntu-ruby-on-rails/

- Ruby: 2.6.3p62
- Gem: 3.0.4
- Sqlite: 3.28.0
- Rails: 5.2.3

Pre-run
- 1st: Copy only the "docker-compose.yml", "Dockerfile", "Gemfile", "Gemfile.lock", "entrypoint.sh" to the desired directory from the "Start docker config"
- 2nd: Check your user id and idgroup running "id" in console.If they are different from 1000 assign those ids in the "dockerfile" options "addgroup(3)", "adduser(4)" and in the "docker-compose.yml" user
- 3rd: Check that the port 3000 is free if not you can change the port in the "dockerfile" expose and "docker-compose.yml" command and port

Run
- 1st: docker-compose run dev rails new --database=postgresql -Jf --skip-coffee .
- 2nd: sudo chown -R $USER:$USER tmp
- 3rd: docker-compose run dev rails new --database=postgresql -Jf --skip-bundle --skip-coffee . -> as the database permissions were set as root 
- 4th: docker-compose build dev -> as "Gemfile" and "Gemfile.lock" have been updated
- 5th: Replace config/database.yml with the one located on the git -> as rails is expecting our database to be in localhost and it is in another container
- 6th: docker-compose run dev rake db:create
- 7th: docker-compose up -d
- 8th: Have fun go to http://localhost:3000 and see the app

Post-Run
- If you ever modify the "dockerfile" or your "Gemfile" you will need to build again the image with a "docker-compose build dev" 

After the environment is prepared you can copy the project to replace the skeleton created

Things left to cover:
* Configuration
* Database creation
* How to run the test suite
* Services (job queues, cache servers, search engines, etc.)
* Deployment instructions
