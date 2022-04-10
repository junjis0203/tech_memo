# RailsコンソールでSQLが出力されるようにする

デフォルトでは`config/environments/production.rb`の`config.log_level`が`:debug`なので初めはSQLが表示されていたが、「ちゃんとログレベル設定」したら出なくなって困った。  
`ActiveRecord::Base.logger`自体を置き換えてしまう例が多いが（[railsdoc](https://railsdoc.com/page/rails_console)にそう書いてあるから？）、ログレベルを変えればいいと思う。`ActiveRecord::Base.logger = Logger.new(STDOUT)`だと日時とかも出力されるので見にくい。

```rb
ActiveRecord::Base.logger.level = :debug
```

debugならSQLが出力される（より正確にはloggerにdebugレベルで書いたものが表示される）
