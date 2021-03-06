# installation, see https://laravel.com/docs/5.5

laravel new project_name
cd project_name

chmod -R a+w storage bootstrap

cp .env.example .env
php artisan key:generate
vim .env # edit .env to set DB_DATABASE, DB_USERNAME, ...

# starting git

git init
git add .
git commit -m"first commit"

# a touch of git flow,
# see http://nvie.com/posts/a-successful-git-branching-model/

git checkout -b develop

# start feature auth from develop

git checkout -b feature/auth develop

# auth scaffolding, see https://laravel.com/docs/5.5/authentication#introduction
# remember to create the database in phpmyadmin before migrating

php artisan make:auth
php artisan migrate

# see changes

git status
gitk --all

# save the step

git add .
git commit -m"auth scaffolding"

# auth feature testing, see https://laravel.com/docs/5.5/testing

php artisan make:test AuthTest

# hint: to list the routes behind "Auth::routes()" in routes/web.php

php artisan route:list

# once tests are written (see https://laravel.com/docs/5.5/http-tests),
# launch them using phpunit

phpunit

# see changes

git status
gitk --all

# save the step

git add .
git commit -m"feature tests for auth"

# merge into develop, and delete the merged branch

git checkout develop
git merge --no-ff feature/auth
git branch -d feature/auth

# time to push

git remote add origin https://github.com/username/project_name.git
git push -u origin master
git push -u origin develop