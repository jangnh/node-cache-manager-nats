<h1>Nats store for cache manager</h1>
<b>This is package use nats jetstream key value bucket</b>
<h3>Install with cache-manager package</h3>
<b>Install</b>
<p>npm install cache-manager</p>
<p>npm install cache-manager-nats-store</p>
<b>Usage Examples</b>
```js
const config = {
    host:"nats://0.0.0.0",
    port:4222,
    ttl: 3600,
    bucket: "test"
}
// Create nats-store
const natsStore = await cacheManager.caching(createBucketKeyValueStore, config);
// set key value
await natsStore.set("test1",{
    id:1,
    value:"Danh",
    age:28
});
// get key
const value = await natsStore.get("test1");
// delete key
await natsStore.del("test1");
// delete all key in bucket
await natsStore.reset();
```
<br/>
<br/>
<br/>
<br/>
<h3>Install with nestjs and cache-manager</h3>
<b>Install</b>
<p>npm install cache-manager</p>
<p>npm install cache-manager-nats-store</p>
<b>Usage Examples</b>
```js
@Module({
  imports: [CacheModule.registerAsync({
    imports: [ConfigModule],
    useFactory: async (configService: ConfigService) => {
      const store = await createBucketKeyValueStore({
        host: configService.get<string>('STARWARS_PALPATINE_NATS_HOST'),
        port: configService.get<number>('STARWARS_PALPATINE_NATS_PORT'),
        bucket: configService.get<string>('STARWARS_PALPATINE_NATS_BUCKET'),
        ttl: 86400 * 30
      })
      return {
        store: store as unknown as CacheStore
      }
    },
    inject: [ConfigService]
  })],
  controllers: [],
  providers: [],
  exports: []
})
export class AppModule {}
```