# Java Persistence

Response Time

Throughput



# Caching Best Practices

Cache Synchronization Strategy
	Cache-aside
		Cache Miss
			get the key from Cache, if not get it from Database and store it in Cache
		Cache Hit
			get the key from Cache
		Cache Update
			update the key in both Cache and Database
		Cons
			Mixing the cache api with the business logic to update cache is not a best practice
	Read Through
		Cache Miss
			get(key) call in Application >> Cache >> Cache Store >> Database
			get the key from Cache Store, if not get it from Database and store it in Cache Store
		Cache Hit
			get the key from Cache
	Write Through
		Cache Update
			put(key, entity) call in Application >> Cache >> Cache Store >> Database
	Write Invalidate
		Cache Update
			put(key, entity) call in Application >> Cache >> Cache Store remove(key) >> Database
	Write Behind
		Cache Update
			put(key, entity) call in Application >> put(key, entity) Cache >> enqueue(key) Cache Store >> Database
		Cache Flush
			flush() Cache >> flush() Cache Store >> Database
			
Caching Layers
	Service Layer	>>	Application Level Cache
	Data Access Layer	>>	Hibernate 2nd Level Cache
	Database Shared Buffers	>>	OS Cache
