# Remineの実験環境をつくる。

0. 同じフォルダに、redmineをチェックアウトする。  
	```
	svn co https://svn.redmine.org/redmine/branches/3.4-stable/ ./redmine
	```  

1. コンテナ起動。  
	```
	docker-compose up -d
	```  

2. Railsサーバにログイン（ほんとはちょっと違うけど）して、
	```
	docker exec -i -t railsdev bash
	```

3. Redmineをセットアップ。
```
bundle install --without development test --path vendor/bundle
bundle exec rake generate_secret_token
bundle exec rake db:migrate
REDMINE_LANG=ja bundle exec rake redmine:load_default_data
```

4. Redmineサーバを起動する。  
	（`-b`つけないと、host側からのアクセスに答えてくれない）  
	```
	bundle exec rails s -b '0.0.0.0'
	```

5. これで、LinuxまたはMacならブラウザで http://localhost:3000/ を開く。
	または、Windowsなら以下のコマンドで`dokcer-machine`でIPを確認して、ブラウザを開く。  
	```
	$ docker-machine ip default
	192.168.99.100
	```
	ならば、http://192.168.99.100:3000/ となる。

# 備考

Dockerfileに改善の余地あり。  
最後にinitをキックしているけど、これ多分、今だとうまく動かない。はず。  

