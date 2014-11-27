#!/bin/bash

name=$1
number=$2
salt=`dd if=/dev/urandom bs=6 count=1`
proper_name="$(tr '[:lower:]' '[:upper:]' <<< ${name:0:1})${name:1}"
server_name=safehouse-$name-`date | xargs echo $salt | md5 | cut -c1-10`

git clone https://github.com/hwayne/safehouse $1
cd $1
heroku create $server_name
git push heroku master
heroku config:set DJANGO_ENVIRONMENT=production
heroku config:set MY_NAME=$proper_name
heroku config:set MY_NUMBER=$number
heroku config:set TWILIO_AUTH_TOKEN=$TWILIO_AUTH_TOKEN
heroku config:set TWILIO_ACCOUNT_SID=$TWILIO_ACCOUNT_SID
heroku addons:add scheduler
heroku run python manage.py syncdb
