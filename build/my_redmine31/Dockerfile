FROM redmine:3.1.7

RUN set -x && \
    # ベースURLを変更
    sed -i \
      -e '/^Rails.application.routes.draw do/a \ scope (Rails.application.config.relative_url_root || "/") do' \
      -e '$i \ end' \
      /usr/src/redmine/config/routes.rb && \
    ln -s . /usr/src/redmine/public/redmine && \
    # 起動時にネットアクセスしないように、bundle install をコメントアウト
    sed -i \
      -e 's/^\([ \t]*bundle install .*\)$/#\1/' \
      /docker-entrypoint.sh && \
    echo done.
