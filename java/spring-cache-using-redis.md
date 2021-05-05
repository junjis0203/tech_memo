# Springでメソッド呼び出しをキャッシュする方法 using Redis

`@Cacheable`や`@EnableCaching`を使えばauto configurationがよしなにやってくれるのだが、キャッシュの有効期限を設定する方法が変わっていてはまった。下記の方法はSpring Boot 2.4.5で動くことを確認。

```java
    @Bean
    // ググるとRedisTemplateを使う方法が出てくるが最近のバージョンではRedisConnectionFactory
    public CacheManager cacheManager(RedisConnectionFactory connectionFactory) {
        RedisCacheConfiguration cacheConfig = RedisCacheConfiguration.defaultCacheConfig()
            // entryTtlを呼ぶと新しいconfigが返される
            .entryTtl(Duration.ofSeconds(60));
        // この書き方は駄目（メソッドを呼び出したオブジェクトは変わらない）
        // cacheConfig.entryTtl(Duration.ofSeconds(60));

        // RedisCacheManagerはbuilderスタイルで作るように変更された
        RedisCacheManager cacheManager = RedisCacheManager.builder(connectionFactory)
            // 上で作成したCacheConfigを設定。キャッシュ名ごとに設定することも可能
            .cacheDefaults(cacheConfig)
            .build();
        return cacheManager;
    }
```
