FROM ruby:3.1.2-buster
RUN sh -c 'echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list' && \
    sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list' && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    curl -sS https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    curl -fsSL https://deb.nodesource.com/setup_11.x | bash - && \
    apt-get update -qq && \
    apt-get install -y nodejs yarn xvfb  vim libnss3 && \
    apt-get -y install google-chrome-stable
RUN CHROMEVER=`google-chrome --version | sed 's/Google Chrome //' | sed 's/\s//'` && \
   wget "https://chromedriver.storage.googleapis.com/`curl https://chromedriver.storage.googleapis.com/LATEST_RELEASE_${CHROMEVER%.*}`/chromedriver_linux64.zip" && \
   yes | unzip chromedriver_linux64.zip && \
   mv -v chromedriver /usr/local/bin/chromedriver && \
   chmod +x /usr/local/bin/chromedriver

#USER www
#WORKDIR /home/www

