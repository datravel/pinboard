# pinboard

Add pinboard user to MySQL:
```
CREATE USER 'pinboard'@'localhost' IDENTIFIED BY 'pinboardPassword';
GRANT ALL PRIVILEGES ON pinba.* TO 'pinboard'@'localhost';
FLUSH PRIVILEGES;
```

Correct settings in the sample files:

- parameters.yml
- fpm-pool.conf
- php.ini

Now you can to run docker container:
```
docker run -d \
--name pinboard \
--net=host \
-w /var/www/pinboard \
-v $(pwd)/parameters.yml:/var/www/pinboard/config/parameters.yml \
-v $(pwd)/php.ini:/etc/php5/fpm/conf.d/99-custom.ini:ro \
-v $(pwd)/fpm-pool.conf:/etc/php5/fpm/pool.d/www.conf:ro \
lebnik/pinboard:latest
```

Now you can restart nginx and open http://pinboard.local/