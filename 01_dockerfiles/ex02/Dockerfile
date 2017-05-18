FROM ruby:2.3.4

# rails necessite nodejs
RUN apt-get update && apt-get install -y nodejs && gem install rails && mkdir -p /opt/app

ONBUILD COPY . /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD EXPOSE 3000
ONBUILD RUN bundle install && rake db:migrate && rake db:seed 

