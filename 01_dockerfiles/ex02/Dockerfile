FROM ruby:onbuild

# rails necessite nodejs
RUN apt-get update && apt-get install -y nodejs && gem install rails && mkdir -p /opt/app

ONBUILD COPY . /opt/app
ONBUILD RUN bundle install && rake db:migrate && rake db:seed 

